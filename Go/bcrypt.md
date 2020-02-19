# Bcrypt
> WIP : 자세한 내용은 추후 Update 될 예정 

비밀번호를 암호화하기 위한 알고리즘중 하나인 Bcrypt에 대해 알아보자.
* Salting
* Key Chaining

### Table of Contents
- [Bcrypt](#bcrypt)
- [main.go](#maingo)
- [index.css](#indexcss)
- [index.html](#indexhtml)
- [signup.html](#signuphtml)
- [login.html](#loginhtml)


## Bcrypt 연습 코드
> 아래는 Bcrypt 를 사용한 User SignUp, LogIn 구현하는 연습 코드 (0219.2020)

Session, Redis, Bcrypt를 사용하여 구현.  
User는 ID, PW를 입력한 후 가입(SignUp)하여 로그인(LogIn)을 해야 Comment를 쓸 수 있다.

 
### main.go
```go
package main

import (
	"fmt"
	"github.com/go-redis/redis"
	"github.com/gorilla/mux"
	"github.com/gorilla/sessions"
	"golang.org/x/crypto/bcrypt"
	"html/template"
	"net/http"
)

type User struct {
	ID       uint32 `json:"id"`
	Email    string `json:"email"`
	Nickname string `json:"nickname,omitempty"`
	Password string `json:"-"`
}

var client *redis.Client  // For reids DB
var store = sessions.NewCookieStore([]byte("teSt-oo20ce20vc")) // Session Our secret Key "teSt-oo20ce20vc"
var templates *template.Template

/* Get Data from Client*/
func main() {
	client = redis.NewClient(&redis.Options{
		Addr: "localhost:6379", // 6379 is the default port number of redis
	})
	templates = template.Must(template.ParseGlob("templates/*.html"))
	r := mux.NewRouter()

	// End Point (This will only use GET method)
	r.HandleFunc("/user/list", listUser).Methods("GET")

	// TESTING POST AND GET Methods
	r.HandleFunc("/", indexGetHandler).Methods("GET")
	r.HandleFunc("/", indexPostHandler).Methods("POST")

	// login (w/ session)
	r.HandleFunc("/login", loginGetHandler).Methods("GET")
	r.HandleFunc("/login", loginPostHandler).Methods("POST")

	// SignUp (w/ Bcrypt)
	r.HandleFunc("/signup", signupGetHandler).Methods("GET")
	r.HandleFunc("/signup", signupPostHandler).Methods("POST")

	// Instantiate File object
	fs := http.FileServer(http.Dir("./static/"))
	// Connect Static File
	r.PathPrefix("/static/").Handler(http.StripPrefix("/static/", fs))

	// Default page
	http.Handle("/", r)
	// Port Number
	http.ListenAndServe(":8080", nil)
}

// Take Input to Struct
func listUser(w http.ResponseWriter, r *http.Request) {
	userList := map[string]string{
		"user":     "Thome",
		"password": "123154",
	}
	// Write on Browser
	fmt.Fprintln(w, userList)
}

func indexGetHandler(w http.ResponseWriter, r *http.Request) {
	session, _ := store.Get(r, "session")
	_, ok := session.Values["username"]
	if !ok {
		http.Redirect(w, r, "/login", 302)
		return
	}

	comments, err := client.LRange("comments", 0, 10).Result()
	if err != nil {
		return
	}

	templates.ExecuteTemplate(w, "index.html", comments) // Pass comments to the templates
}

func indexPostHandler(w http.ResponseWriter, r *http.Request) {
	r.ParseForm()
	comment := r.PostForm.Get("comment")
	client.LPush("comments", comment) //Redis Commands
	http.Redirect(w, r, "/", 302)
}

func loginGetHandler(w http.ResponseWriter, r *http.Request) {
	templates.ExecuteTemplate(w, "login.html", nil)
}

// After user Push the login-submit button than New page will show up
func loginPostHandler(w http.ResponseWriter, r *http.Request) {
	r.ParseForm()
	username := r.PostForm.Get("username")
	// Bcrypt : Hash Password
	password := r.PostForm.Get("password")
	hash, err := client.Get("user:" + username).Bytes()
	if err != nil {
		return
	}
	err = bcrypt.CompareHashAndPassword(hash, []byte(password))
	// if password incorrect
	if err != nil {
		return
	}

	// Session
	session, _ := store.Get(r, "session")
	session.Values["username"] = username
	session.Save(r, w)
	http.Redirect(w, r, "/", 302)
}

func signupGetHandler(w http.ResponseWriter, r *http.Request) {
	templates.ExecuteTemplate(w, "signup.html", nil)
}

// Create New User
func signupPostHandler(w http.ResponseWriter, r *http.Request) {
	r.ParseForm()
	username := r.PostForm.Get("username")
	password := r.PostForm.Get("password")

	// Bcrypt
	cost := bcrypt.DefaultCost
	hash, err := bcrypt.GenerateFromPassword([]byte(password), cost) // to use bcrpyt we need to convert string password to byte
	if err != nil {
		return
	}
	client.Set("user:" + username, hash, 0) // 0 it's mean expired.
	http.Redirect(w, r, "/login", 302)
}
```

[Return to TOC](#table-of-contents) 


### index.css
```css
body > div {
     padding: 0.5em;
     width: 200px;
     margin: 1em 0em;
     background:  #ccc;
     border: 1px solid #aaa;
 }
```

[Return to TOC](#table-of-contents) 


### index.html
```html
<html>
    <head>
        <title>Comments</title>
        <link rel="stylesheet" type="text/css" href="/static/index.css">
    </head>
    <body>
        <h1>Comments</h1>
        <form method="POST">
            <textarea name="comment"></textarea>
            <div>
                <button type="submit">Post Comment</button>
            </div>
        </form>
        {{range .}}
            {{/*            loop over the value we passed (in this case . is the comment) */}}
        <div>{{.}}</div>
            {{/*                contains the string*/}}
        {{end}}
    </body>
</html>
```

[Return to TOC](#table-of-contents) 


### signup.html
```html
<html>
<head>
    <title>SignUp</title>
</head>
<body>
    <form method="POST">
        <div>
            Username : <input name="username">
        </div>
        <div>
            Password : <input name="password">
        </div>
        <div>
            <button type="submit">SignUp</button>
        </div>
    </form>
</body>
</html>
```

[Return to TOC](#table-of-contents) 


### login.html
```html
<head>
    <title>LogIn</title>
</head>
    <body>
    <form method="POST">
        <div>
            Username : <input name="username">
        </div>
        <div>
            Password : <input name="password">
        </div>
        <div>
            <button type="submit">LogIn</button>
        </div>
    </form>
    </body>
</html>
```

[Return to TOC](#table-of-contents) 
