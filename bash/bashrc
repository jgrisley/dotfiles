
shopt -s cdspell
shopt -s no_empty_cmd_completion

if_os () {
    [[ $OSTYPE == *$1* ]];
}

if_nix () {
    case "$OSTYPE" in
        *linux*|*hurd*|*msys*|*cygwin*|*sua*|*interix*) sys="gnu";;
        *bsd*|*darwin*) sys="bsd";;
        *sunos*|*solaris*|*indiana*|*illumos*|*smartos*) sys="sun";;
    esac
    [[ "${sys}" == "$1" ]];
}


set_bsd_ls_colors () {
    CLICOLORS=on
    # emulate GNU ls default colors in BSD/Darwin
    # LSCOLORS
    # The value of this variable describes what color to use
    # for which attribute when colors are enabled with
    # CLICOLOR.  This string is a concatenation of pairs of the
    # format fb, where f is the foreground color and b is the
    # background color.
    #
    # The color designators are as follows:
    #     a   black      | A   bold black, usually shows up as dark grey
    #     b   red        | B   bold red
    #     c   green      | C   bold green
    #     d   brown      | D   bold brown, usually shows up as yellow
    #     e   blue       | E   bold blue
    #     f   magenta    | F   bold magenta
    #     g   cyan       | G   bold cyan
    #     h   light grey | H   bold light grey; looks like bright white
    #
    #     x   default foreground or background
    #
    # Note that the above are standard ANSI colors.  The actual
    # display can differ depending on the color capabilities of
    # the terminal in use.
    # The order of the attributes are as follows:
    # 1.  directory
    LSCOLORS="Ex" # bold blue
    # 2.  symbolic link
    LSCOLORS+="Gx"
    # 3.  socket
    LSCOLORS+="Bx"
    # 4.  pipe
    LSCOLORS+="Dx"
    # 5.  executable
    LSCOLORS+="Cx" # bold green
    # 6.  block special
    LSCOLORS+="Eg"
    # 7.  character special
    LSCOLORS+="Ed"
    # 8.  executable with setuid bit set
    LSCOLORS+="xb"
    # 9.  executable with setgid bit set
    LSCOLORS+="xg"
    # 10.  directory writable to others, with sticky bit
    LSCOLORS+="xc"
    # 11.  directory writable to others, without sticky bit
    LSCOLORS+="xd"
    # The default is "exfxcxdxbxegedabagacad",

    # alias ls for colors in BSD/Darwin
    alias ls='ls -Gp'
}

set_gnu_ls_colors () {
    alias ls='ls --color=auto'
    # To have colors for ls and all grep commands such as grep, egrep and zgrep
    #export LS_COLORS='no=00:fi=00:di=00;34:ln=01;36:pi=40;33:so=01;35:do=01;35:bd=40;33;01:cd=40;33;01:or=40;31;01:ex=01;32:*.tar=01;31:*.tgz=01;31:*.arj=01;31:*.taz=01;31:*.lzh=01;31:*.zip=01;31:*.z=01;31:*.Z=01;31:*.gz=01;31:*.bz2=01;31:*.deb=01;31:*.rpm=01;31:*.jar=01;31:*.jpg=01;35:*.jpeg=01;35:*.gif=01;35:*.bmp=01;35:*.pbm=01;35:*.pgm=01;35:*.ppm=01;35:*.tga=01;35:*.xbm=01;35:*.xpm=01;35:*.tif=01;35:*.tiff=01;35:*.png=01;35:*.mov=01;35:*.mpg=01;35:*.mpeg=01;35:*.avi=01;35:*.fli=01;35:*.gl=01;35:*.dl=01;35:*.xcf=01;35:*.xwd=01;35:*.ogg=01;35:*.mp3=01;35:*.wav=01;35:*.xml=00;31:'
}

export GREP_OPTIONS='--color=auto'
export GREP_COLOR='1;32'
export CLICOLOR=1

if_nix gnu  && set_gnu_ls_colors
if_nix bsd && set_bsd_ls_colors && export CLICOLORS=$CLICOLORS && export LSCOLORS=$LSCOLORS

# Setup history for unlimited size
# and eternal history
HISTCONTROL=erasedups
HISTFILESIZE=
HISTSIZE=
HISTTIMEFORMAT="[%h%d %a %r] "
HISTFILE=~/.bash_eternal_history

#tput Colour Capabilities
#tput setab [1-7] #Set a background colour using ANSI escape
b_grey="\[$(tput setab 0)\]"
b_red="\[$(tput setab 1)\]"
b_green="\[$(tput setab 2)\]"
b_yellow="\[$(tput setab 3)\]"
b_blue="\[$(tput setab 4)\]"
b_magenta="\[$(tput setab 5)\]"
b_cyan="\[$(tput setab 6)\]"
b_white="\[$(tput setab 7)\]"
#tput setb [1-7] #Set a background colour
#tput setaf [1-7] #Set a foreground colour using ANSI escape
f_grey="\[$(tput setaf 0)\]"
f_red="\[$(tput setaf 1)\]"
f_green="\[$(tput setaf 2)\]"
f_yellow="\[$(tput setaf 3)\]"
f_blue="\[$(tput setaf 4)\]"
f_magenta="\[$(tput setaf 5)\]"
f_cyan="\[$(tput setaf 6)\]"
f_white="\[$(tput setaf 7)\]"
#tput setf [1-7] #Set a foreground colour

#tput Text Mode Capabilities
#tput bold #Set bold mode
bold="\[$(tput bold)\]"
#tput dim #turn on half-bright mode
#tput smul #begin underline mode
#tput rmul #exit underline mode
#tput rev #Turn on reverse mode
#tput smso #Enter standout mode (bold on rxvt)
#tput rmso #Exit standout mode
#tput sgr0 #Turn off all attributes (doesn't work quite as expected)
reset="\[$(tput sgr0)\]"

promptstatus () {
    if [ "$?" -ne "0" ]; then
        echo $(printf "╠%s\n" $?)
    else
        echo ''
    fi
}

status_fmt () {
    if [ "$?" -ne "0" ]; then
        echo "$(tput setaf 1)☠"
    else
        echo "$(tput setaf 2)▷"
    fi
}

trim_cmd () {
    export H1="$(history 1 | sed -e "s/^ \+//g; s/^[\ 0-9]*//; s/^\[.*\]//; s/[\d0\d31\d34\d39\d96\d127]*//g; s/\(.\{1,50\}\).*$/\1/g")";
}

PROMPT_COMMAND='trim_cmd; history -a;'

PS1="\n${reset}${bold}${f_grey}╔══[${reset}${f_grey}\j:\!:\#${reset}${bold}${f_grey}]${reset}${f_cyan}\T \d${reset}${bold}${f_grey}[${reset}${f_blue}\u@\H ${f_green}+${SHLVL}${bold}${f_grey}]${reset}${bold}${f_white} \w \n${reset}${bold}${f_grey}╚${reset}\$(status_fmt)\$${reset} "

#-----------------------------------------------------------------------
# alias system commands
#-----------------------------------------------------------------------

# cd
alias c='cd'
alias c-='cd -'
alias u1='cd ../'
alias u2='cd ../../'
alias u3='cd ../../../'
alias u4='cd ../../../../'
alias u5='cd ../../../../../'
alias u6='cd ../../../../../../'
alias u7='cd ../../../../../../../'
alias u8='cd ../../../../../../../../'
#alias cd  =       'cd \!*    ; setprompt'
#alias pushd =     'pushd \!* ; setprompt'
#alias popd  =     'popd \!*  ; setprompt'

# general
alias cls=clear
alias cmore='clear; more '
alias cpr='cp -pr'
alias d='date'
alias g='grep'
alias m='more'
alias le='less'
alias h=history
alias hg='history|grep'
alias mkd=mkdir
alias rmr='rm -r'
alias rmrf='rm -rf'
alias t='tail'
alias rm='rm -i'
alias cp='cp -i'
alias rl='rlogin'
#alias bye	logout

# gvim
alias gv="gvim -u ${HOME}/.vimrc"
alias gvi="gvim -u ${HOME}/.vimrc"
alias givm="gvim -u ${HOME}/.vimrc"
alias gvim="gvim -u ${HOME}/.vimrc"
alias gvd='gvimdiff'
alias gvn='gvim --noplugin'

# perl
alias formatperl='perltidy -i=2 -ci=2 -sil=1 -bt=2 -pt=2 -sbt=2 -bbt=2 -nsak="if elsif" -l=80  -nsbl -nsfs -nbbc -lp -vt=1 -vtc=0 -sbc -nolc -nwls="." -nwrs="." -nolq -mft=3'

# tdkiff
alias tkd='tkdiff'

# xterm
alias xtrm='xterm -bg black -bd green -fg green -fn Courier -title ~ &'

