# ~/.bashrc: executed by bash(1) for non-login shells.
# see /usr/share/doc/bash/examples/startup-files (in the package bash-doc)
# for examples

# If not running interactively, don't do anything
case $- in
    *i*) ;;
      *) return;;
esac

# don't put duplicate lines or lines starting with space in the history.
# See bash(1) for more options
HISTCONTROL=ignoreboth

# append to the history file, don't overwrite it
shopt -s histappend

# for setting history length see HISTSIZE and HISTFILESIZE in bash(1)
HISTSIZE=1000
HISTFILESIZE=2000

# check the window size after each command and, if necessary,
# update the values of LINES and COLUMNS.
shopt -s checkwinsize

# If set, the pattern "**" used in a pathname expansion context will
# match all files and zero or more directories and subdirectories.
#shopt -s globstar

# make less more friendly for non-text input files, see lesspipe(1)
#[ -x /usr/bin/lesspipe ] && eval "$(SHELL=/bin/sh lesspipe)"

# set variable identifying the chroot you work in (used in the prompt below)
if [ -z "${debian_chroot:-}" ] && [ -r /etc/debian_chroot ]; then
    debian_chroot=$(cat /etc/debian_chroot)
fi

# set a fancy prompt (non-color, unless we know we "want" color)
case "$TERM" in
    xterm-color) color_prompt=yes;;
esac

# uncomment for a colored prompt, if the terminal has the capability; turned
# off by default to not distract the user: the focus in a terminal window
# should be on the output of commands, not on the prompt
#force_color_prompt=yes

if [ -n "$force_color_prompt" ]; then
    if [ -x /usr/bin/tput ] && tput setaf 1 >&/dev/null; then
	# We have color support; assume it's compliant with Ecma-48
	# (ISO/IEC-6429). (Lack of such support is extremely rare, and such
	# a case would tend to support setf rather than setaf.)
	color_prompt=yes
    else
	color_prompt=
    fi
fi

if [ "$color_prompt" = yes ]; then
    PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '
else
    PS1='${debian_chroot:+($debian_chroot)}\u@\h:\w\$ '
fi
unset color_prompt force_color_prompt

# If this is an xterm set the title to user@host:dir
case "$TERM" in
xterm*|rxvt*)
    PS1="\[\e]0;${debian_chroot:+($debian_chroot)}\u@\h: \w\a\]$PS1"
    ;;
*)
    ;;
esac

# enable color support of ls and also add handy aliases
if [ -x /usr/bin/dircolors ]; then
    test -r ~/.dircolors && eval "$(dircolors -b ~/.dircolors)" || eval "$(dircolors -b)"
    alias ls='ls --color=auto'
    #alias dir='dir --color=auto'
    #alias vdir='vdir --color=auto'

    #alias grep='grep --color=auto'
    #alias fgrep='fgrep --color=auto'
    #alias egrep='egrep --color=auto'
fi

# colored GCC warnings and errors
#export GCC_COLORS='error=01;31:warning=01;35:note=01;36:caret=01;32:locus=01:quote=01'

# some more ls aliases
#alias ll='ls -l'
#alias la='ls -A'
#alias l='ls -CF'

# Alias definitions.
# You may want to put all your additions into a separate file like
# ~/.bash_aliases, instead of adding them here directly.
# See /usr/share/doc/bash-doc/examples in the bash-doc package.

if [ -f ~/.bash_aliases ]; then
    . ~/.bash_aliases
fi

# enable programmable completion features (you don't need to enable
# this, if it's already enabled in /etc/bash.bashrc and /etc/profile
# sources /etc/bash.bashrc).
if ! shopt -oq posix; then
  if [ -f /usr/share/bash-completion/bash_completion ]; then
    . /usr/share/bash-completion/bash_completion
  elif [ -f /etc/bash_completion ]; then
    . /etc/bash_completion
  fi
fi

# java
export JAVA_HOME=/opt/jdk1.7.0
export JRE_HOME=${JAVA_HOME}/jre
export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib:${SPARK_HOME}/lib
export PATH=${JAVA_HOME}/bin:$PATH
# tomcat
export TOMCAT_HOME=/opt/tomcat8.0
export PATH=$TOMCAT_HOME/bin:$PATH
# ant
export ANT_HOME=/opt/apache-ant-1.9.7
export PATH=$ANT_HOME/bin:$PATH
# maven
export M2_HOME=/opt/apache-maven-3.2.2
export PATH=$M2_HOME/bin:$PATH
# findbugs
export FINDBUGS_HOME=/opt/findbugs-3.0.1.tar.gz
export PATH=$FINDBUGS_HOME/bin:$PATH
# hadoop
export HADOOP_HOME=/home/rocky/workspace/hadoop-2.6.0
export PATH=$HADOOP_HOME/bin:$HADOOP_HOME/sbin:$HADOOP_HOME/lib:$PATH
# HBase
export HBASE_HOME=/home/rocky/hbase/hbase-1.0.0
export PATH=$HBASE_HOME/bin:$PATH
# HIVE
export HIVE_HOME=/home/rocky/hive/apache-hive-1.0.1-bin
export PATH=$HIVE_HOME/bin:$PATH

# scala 
export SCALA_HOME=/opt/scala-2.11.6
export PATH=${SCALA_HOME}/bin:$PATH
# spark
export SPARK_HOME=~/spark-1.4.1-bin-hadoop2.6
#export CLASSPATH=.:${SPARK_HOME}/lib
export PATH=${SPARK_HOME}/sbin:${SPARK_HOME}/bin:${SPARK_HOME}/lib:$PATH


# datascience
export PATH=/home/rocky/git/data-science-at-the-command-line/tools:$PATH

# xml2json nodejs
export PATH=/usr/share/node_modules/xml2json-command/node_modules/xml-mapping/examples:$PATH

# json2csv golang leiningen
export PATH=/home/rocky/tools/bin:$PATH

# drake drip
export PATH=/home/rocky/tools/drip/bin:$PATH
export HTTP_CLIENT="wget --no-check-certificate -O"

names() { sed -e 's/,/\n/g;q'; }
