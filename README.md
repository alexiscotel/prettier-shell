# Prettier shell

PS1 prompt for ~/.bashrc file

## format
### Date : `\A`
- <span style="color: #808080">grey 80</span>
	```bash
	PS1='\[\e[38;5;249m\]\A\[\e[0m\]'
	```
- <span style="color: #c0c0c0">grey c0</span>
	```bash
	PS1='\[\e[38;5;251;1m\]\A\[\e[0m\]'
	```

### function to get OS distribution name
```bash
# OS Distribution name
get_os_name() {
     FILE=/etc/os-release
     if test -f "$FILE"; then
         awk -F= '$1=="ID" { print " "$2 ;}' "$FILE"
     fi
}
```
Color : <span style="color: #feffd9; background-color: black; padding: 2px 5px">light yellow</span>
```bash
PS1='\[\e[38;5;230;2m\]$(get_os_name)\[\e[0m\]'
```

### username `\u`
- <span style="color: #2983fb">blue</span>
```bash
PS1='\[\e[38;5;33;3m\]\u\[\e[0m\]'
```
- <span style="color: #d5b12a">orange</span>
```bash
PS1='\[\e[38;5;178m\]\u\[\e[0m\]'
```
- <span style="color: #d72118">red</span>
```bash
PS1='\[\e[38;5;160;1;5m\]\u\[\e[0m\]'
```

### @ (simple text)
Color: <span style="color: white; font-weight: bold; background-color: black; padding: 2px 5px">white</span>
```bash
PS1='\[\e[97;1m\]@\[\e[0m\]'
```

### hostname `\H`
- <span style="color: #00ae1f">Green</span>
```bash
PS1='\[\e[38;5;34m\]\H\[\e[0m\]'
```

### path `\w`
- <span style="color: #d4d831">Yellow</span>
```bash
PS1='\[\e[0;38;5;184m\]\w\[\e[0m\]'
```

### function to get actual git branch
- <span style="color: #1bd4fc">Turquoise</span>
```bash
# git branch
parse_git_branch() {
	git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1) /'
}
PS1='\[\e[0;3;38;5;45m\]$(parse_git_branch)\[\e[0m\]'
```

## PS1 prompt
### Without colors
```bash
PS1='\A $(get_os_name) \u@\H \w $(parse_git_branch) 💨 '
```

### With colors
Date & OS
```bash
\[\e[38;5;251;1m\]\A\[\e[0m\] \[\e[38;5;230;2m\]$(get_os_name)\[\e[0m\]
```
username & hostname
- external (blue)
```bash
\[\e[38;5;33;3m\]\u\[\e[0m\]\[\e[97;1m\]@\[\e[0m\]\[\e[38;5;34m\]\H\[\e[0m\]
```
- internal (orange)
```bash
\[\e[38;5;178m\]\u\[\e[0m\]\[\e[97;1m\]@\[\e[0m\]\[\e[38;5;34m\]\H\[\e[0m\]
```
- root (red)
```bash
\[\e[38;5;160;1;5m\]\u\[\e[0m\]\[\e[97;1m\]@\[\e[0m\]\[\e[38;5;34m\]\H\[\e[0m\]
```
path & git branch
```bash
\[\e[0;38;5;184m\]\w\[\e[0m\] \[\e[0;3;38;5;45m\]$(parse_git_branch)\[\e[0m\]
```
### PS1
- external (blue username)
```bash
PS1='\[\e[38;5;251;1m\]\A\[\e[0m\]\[\e[38;5;230;2m\]$(get_os_name)\[\e[0m\] \[\e[38;5;33;3m\]\u\[\e[0m\]\[\e[97;1m\]@\[\e[0m\]\[\e[38;5;34m\]\H\[\e[0m\] \[\e[0;38;5;184m\]\w\[\e[0m\] \[\e[0;3;38;5;45m\]$(parse_git_branch)\[\e[0m\]'
```
- internal (orange username)
```bash
PS1='\[\e[38;5;251;1m\]\A\[\e[0m\]\[\e[38;5;230;2m\]$(get_os_name)\[\e[0m\] \[\e[38;5;178m\]\u\[\e[0m\]\[\e[97;1m\]@\[\e[0m\]\[\e[38;5;34m\]\H\[\e[0m\] \[\e[0;38;5;184m\]\w\[\e[0m\] \[\e[0;3;38;5;45m\]$(parse_git_branch)\[\e[0m\]'
```
- root (red blinking username)
```bash
PS1='\[\e[38;5;251;1m\]\A\[\e[0m\]\[\e[38;5;230;2m\]$(get_os_name)\[\e[0m\] \[\e[38;5;160;1;5m\]\u\[\e[0m\]\[\e[97;1m\]@\[\e[0m\]\[\e[38;5;34m\]\H\[\e[0m\] \[\e[0;38;5;184m\]\w\[\e[0m\] \[\e[0;3;38;5;45m\]$(parse_git_branch)\[\e[0m\]'
```

### Global
```bash
### PERSONNAL CONFIGURATION
# git branch
parse_git_branch() {
	git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1) /'
}

# OS Distribution name
get_os_name() {
     FILE=/etc/os-release
     if test -f "$FILE"; then
         awk -F= '$1=="ID" { print " "$2 ;}' "$FILE"
     fi
}

# External User
PS1='\[\e[38;5;251;1m\]\A\[\e[0m\]\[\e[38;5;230;2m\]$(get_os_name)\[\e[0m\] \[\e[38;5;33;3m\]\u\[\e[0m\]\[\e[97;1m\]@\[\e[0m\]\[\e[38;5;34m\]\H\[\e[0m\] \[\e[0;38;5;184m\]\w\[\e[0m\] \[\e[0;3;38;5;45m\]$(parse_git_branch)\[\e[0m\]
💨 '

# Internal User
#PS1='\[\e[38;5;251;1m\]\A\[\e[0m\]\[\e[38;5;230;2m\]$(get_os_name)\[\e[0m\] \[\e[38;5;178m\]\u\[\e[0m\]\[\e[97;1m\]@\[\e[0m\]\[\e[38;5;34m\]\H\[\e[0m\] \[\e[0;38;5;184m\]\w\[\e[0m\] \[\e[0;3;38;5;45m\]$(parse_git_branch)\[\e[0m\]
#💨 '

# Root (red blinking)
#PS1='\[\e[38;5;251;1m\]\A\[\e[0m\]\[\e[38;5;230;2m\]$(get_os_name)\[\e[0m\] \[\e[38;5;160;1;5m\]\u\[\e[0m\]\[\e[97;1m\]@\[\e[0m\]\[\e[38;5;34m\]\H\[\e[0m\] \[\e[0;38;5;184m\]\w\[\e[0m\] \[\e[0;3;38;5;45m\]$(parse_git_branch)\[\e[0m\]
#💨 '
```


### External user (blue)
```bash
### PERSONNAL CONFIGURATION
# git branch
parse_git_branch() {
	git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1) /'
}

# OS Distribution name
get_os_name() {
     FILE=/etc/os-release
     if test -f "$FILE"; then
         awk -F= '$1=="ID" { print " "$2 ;}' "$FILE"
     fi
}

# External User
PS1='\[\e[38;5;251;1m\]\A\[\e[0m\]\[\e[38;5;230;2m\]$(get_os_name)\[\e[0m\] \[\e[38;5;33;3m\]\u\[\e[0m\]\[\e[97;1m\]@\[\e[0m\]\[\e[38;5;34m\]\H\[\e[0m\] \[\e[0;38;5;184m\]\w\[\e[0m\] \[\e[0;3;38;5;45m\]$(parse_git_branch)\[\e[0m\]
💨 '
```
### Internal user (orange)
```bash
### PERSONNAL CONFIGURATION
# git branch
parse_git_branch() {
	git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1) /'
}

# OS Distribution name
get_os_name() {
     FILE=/etc/os-release
     if test -f "$FILE"; then
         awk -F= '$1=="ID" { print " "$2 ;}' "$FILE"
     fi
}

# Internal User
PS1='\[\e[38;5;251;1m\]\A\[\e[0m\]\[\e[38;5;230;2m\]$(get_os_name)\[\e[0m\] \[\e[38;5;178m\]\u\[\e[0m\]\[\e[97;1m\]@\[\e[0m\]\[\e[38;5;34m\]\H\[\e[0m\] \[\e[0;38;5;184m\]\w\[\e[0m\] \[\e[0;3;38;5;45m\]$(parse_git_branch)\[\e[0m\]
💨 '
```


### for root (red blinking)
```bash
### PERSONNAL CONFIGURATION
# git branch
parse_git_branch() {
	git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1) /'
}

# OS Distribution name
get_os_name() {
     FILE=/etc/os-release
     if test -f "$FILE"; then
         awk -F= '$1=="ID" { print " "$2 ;}' "$FILE"
     fi
}

# Root (red blinking)
PS1='\[\e[38;5;251;1m\]\A\[\e[0m\]\[\e[38;5;230;2m\]$(get_os_name)\[\e[0m\] \[\e[38;5;160;1;5m\]\u\[\e[0m\]\[\e[97;1m\]@\[\e[0m\]\[\e[38;5;34m\]\H\[\e[0m\] \[\e[0;38;5;184m\]\w\[\e[0m\] \[\e[0;3;38;5;45m\]$(parse_git_branch)\[\e[0m\]
💥 '
```