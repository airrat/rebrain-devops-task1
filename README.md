## Анимированная новогодняя елка

![Новогодняя елка](/xmas/screenshot.jpg)

## Установка и запуск

1.  Скачиваем сам скрипт.

|     |     |
| --- | --- |
| wget | `wget https://github.com/airrat/rebrain-devops-task1/blob/master/xmas/xmas.sh` |
| curl | `curl -O https://github.com/airrat/rebrain-devops-task1/blob/master/xmas/xmas.sh` |

2.  Делаем скрипт исполняемым:
    `chmod +x xmas.sh`
3.  Запускаем скирпт:
    `./xmas.sh`
4.  Выходим из скрипта, нажав `CTRL` \+ `c`

## Использование

### Содержимое скрипта.

```bash
# The following line tells the shell what program to interpret the script with
#!/bin/bash
# tput is a command to manipulate the terminal, it can be used to change the color of text, apply effects, and generally brighten things up.
trap "tput reset; tput cnorm; exit" 2
clear
tput civis
lin=2
col=$(($(tput cols) / 2))
c=$((col-1))
est=$((c-2))
color=0
# Set the text color to green to write the tree
tput setaf 2; tput bold
# Write the tree
for ((i=1; i<40; i+=2))
{
    tput cup $lin $col
    for ((j=1; j<=i; j++))
    {
        echo -n \*
    }
    let lin++
    let col--
}
# Set the color to brown for the trunk
tput sgr0; tput setaf 130
# Write the Trunk in three lines
for ((i=1; i<=3; i++))
{
    tput cup $((lin++)) $c
    echo 'mWm'
}
# Write a greeting
tput setaf 93; tput bold
tput cup $lin $((c - 15)); echo SCALEWAY wishes you Merry Christmas
tput cup $((lin + 1)) $((c - 11)); echo And a Happy New Year 2024
let c++
k=1
# Configure lights and decorations
while true; do
    for ((i=1; i<=35; i++)) {
        # Turn off the lights
        [ $k -gt 1 ] && {
            tput setaf 2; tput bold
            tput cup ${line[$[k-1]$i]} ${column[$[k-1]$i]}; echo \*
            unset line[$[k-1]$i]; unset column[$[k-1]$i]  # Array cleanup
        }
        li=$((RANDOM % 9 + 10))
        start=$((c-li+2))
        co=$((RANDOM % (li-2) * 2 + 1 + start))
        tput setaf $color; tput bold   # Switch colors
        tput cup $li $co
        echo o
        line[$k$i]=$li
        column[$k$i]=$co
        color=$(((color+1)%8))
    }
    k=$((k % 2 + 1))
done
```

### Как это выглядит

<img src="/xmas/scaleway-animated-tree.gif" width="400px">

### Изменяем внешний вид елки

`vim ./xmas.sh`

- *Цвет елки \- `# Set the text color to green to write the tree`*
- *Рисуем елку \- `# Write the tree`*
- *Цвет ствола \- `# Set the color to brown for the trunk`*
- *Рисуем ствол \- `# Write the Trunk in three lines`*
- *Смена текста \- `# Write a greeting`*
- *Смена анимации \- `# Configure lights and decorations`*

## Авторы

[scaleway](https://www.scaleway.com/en/docs/tutorials/bash-christmas-tree/)

## License

[MIT](https://tldrlegal.com/license/mit-license)
