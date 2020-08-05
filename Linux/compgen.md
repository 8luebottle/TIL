# compgen
compgen == **Comp**lete + **Gen**erate

```compgen``` 명령어를 통해 Linux 의 명령어를 볼 수 있다. 

### Table of Contents
- [compgen Options](#compgen-options)
  - [a](#-a) : alias
  - [b](#-b) : builtins
  - [c](#-c) : commands
  - [d](#-d) : directory
  - [e](#-e) : exported
  - [f](#-f) : functions
  - [g](#-g) : groups
  - [j](#-j) : job
  - [k](#-k) : keywords
  - [s](#-s) : service
  - [u](#-u) : userAlias
  - [v](#-v) : variables


## compgen Options 
compgen 명령어와 함께 쓸수 있는 옵션값은 아래와 같다.

* -a
* -b
* -c
* -d
* -e
* -f
* -g
* -j
* -k
* -s
* -u
* -v

[↑ return to TOC](#table-of-contents)

### -a
**a**lias 

```compgen -a | column```  
alias 를 컬럼 형태로 출력한 결과
```
history			gmom			ga			gap
glgga			glod			gb			gapa
gcsm			g			gc			lzd
gbsb			glog			gd			gcan!
groh			gra			gf			gpoat
md			grb			gts			gau
gupv			l			gg			gav
gupav			glol			git-svn-dcommit-push	gcount
gbsg			gga			gdca			gma
gds			grh			gstaa			glum
gbsr			grset			gtv			grmc
gignored		grm			gk			gba
gdt			gwip			gl			grba
gbss			grrm			gm			gbd
gdw			gclean			ggsup			grbc
gpd			grs			gp			which-command
gsps			grt			gr			grbd
gpf			gru			run-help		grbi
-			ggpush			glgg			gbl
gpf!			grv			gdct			grbm
glola			gcn!			gdcw			gmt
1			gsb			glgm			ofd
2			gsd			glgp			gbr
3			gsh			gup			grmv
4			gsi			grup			gbs
5			ghh			gbnm			grbs
6			gcam			pyfind			showfiles
pygrep			grhh			gunwip			gca
7			gsr			gignore			gcb
8			gss			ggpur			la
pip			gst			gke			gunignore
9			gsu			gloga			gcd
gpu			gsta			gbda			gcf
gpv			grss			gswc			gcmsg
gcans!			gpsup			gmtvim			python
grep			gsw			ggpull			afind
lsa			gstc			gcpa			gcl
glols			gstd			gcpc			globurl
grev			glods			gwch			gcm
gca!			gstl			gaa			ll
hidefiles		gstp			glg			gco
gfa			gsts			gc!			gcp
gfg			gstu			gbD			gupa
gpristine		rd			glo			gcs
gfo			gtl			glp			ls
_			gstall			gmum
```

[↑ return to TOC](#table-of-contents)


### -b
shell **b**uiltins

```compgen -b | column```  
shell builtins 를 컬럼 형태로 출력한 결과

```
unset		sysopen		compctl		print		enable		kill
zsocket		sched		r		zf_rm		limit		compcall
rehash		setopt		zmodload	declare		zf_mv		where
popd		getln		sysseek		comptry		echotc		fg
ulimit		builtin		syswrite	alias		echo		zformat
local		let		zregexparse	shift		wait		suspend
jobs		bg		history		-		dirs		unlimit
disable		zstat		return		.		syserror	break
[		which		exec		bindkey		unsetopt	set
compfiles	unhash		compadd		typeset		read		continue
printf		pwd		emulate		true		:		command
autoload	zparseopts	chdir		hash		integer		zcompile
noglob		logout		ttyctl		strftime	bye		whence
pushln		disown		test		compset		echoti		umask
zle		type		comparguments	cd		compquote	sysread
readonly	source		pushd		compvalues	unfunction	trap
exit		eval		functions	getopts		fc		zsystem
false		compdescribe	float		compgroups	vared		private
times		comptags	zstyle		export		unalias		log
```

[↑ return to TOC](#table-of-contents)


### -c
**c**ommands


[↑ return to TOC](#table-of-contents)


### -d 
**d**irectory

[↑ return to TOC](#table-of-contents)


### -e
**e**xported shell variables

[↑ return to TOC](#table-of-contents)


### -f
**f**unctions

[↑ return to TOC](#table-of-contents)


### -g
**g**roups

[↑ return to TOC](#table-of-contents)


### -j
**j**ob

[↑ return to TOC](#table-of-contents)


### -k
**k**eywords

```compgen -k | column```  
keywords 를 컬럼 형태로 출력한 결과

```
if		end		select		[[		esac		elif
export		do		readonly	repeat		until
declare		typeset		coproc		done		local
function	then		}		for		fi
else		integer		!		while		nocorrect
float		{		case		time		foreach
```

[↑ return to TOC](#table-of-contents)


### -s
**s**ervice

[↑ return to TOC](#table-of-contents)


### -u
**u**serAlias names

-생략-

[↑ return to TOC](#table-of-contents)


### -v
shell **v**ariables

[↑ return to TOC](#table-of-contents)
