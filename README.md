# Usage of Loop, Function and Array in Bash



## Array
```
#Show items and index from an array
declare -a my_array
my_array=(foo bar)
echo ${my_array[@]} #show as "foo bar"
echo ${my_array[*]}  #same as the above for this case
echo ${!my_array[@]} #show as 0 1
echo ${!my_array[*]} #same as the above for this case

#Show items and index from an "key-value" array
declare -a my_array3
my_array3=([foo]="str1" [bar]="str2")
echo ${my_array3[@]}
echo ${!my_array3[@]}
```

## Loop 
```
#For Loop
declare -a my_array5
my_array5=([foo]="str1" [bar]="str2")
for key in "${!my_array5[@]}"; do echo "$key"; done

#While Loop
cyberciti.biz|202.54.1.1|/home/httpd|ftpcbzuser
nixcraft.com|202.54.1.2|/home/httpd|ftpnixuser
Create a shell script called setupapachevhost.sh as follows:

#!/bin/bash
# setupapachevhost.sh - Apache webhosting automation demo script
file=/tmp/domains.txt

# set the Internal Field Separator to |
IFS='|'
while read -r domain ip webroot ftpusername
do
        printf "*** Adding %s to httpd.conf...\n" $domain
        printf "Setting virtual host using %s ip...\n" $ip
        printf "DocumentRoot is set to %s\n" $webroot
        printf "Adding ftp access for %s using %s ftp account...\n\n" $domain $ftpusername
	
done < "$file"

```

## Function

### Example: get the unique values from a list
#Copied from https://github.com/dylanaraps/pure-bash-bible

echo "usage: remove_array_dups 1 1 2 2 3 3 3 3 3 4 4 4 4 4 5 5 5 5 5 5"
echo "result: 1 2 3 4 5"
echo "Usage 2: arr=(red red green blue blue) && remove_array_dups \"\${arr[@]}\" "
echo "result: red green blue"

remove_array_dups() {
    # Usage: remove_array_dups "array"
    declare -A tmp_array
    #echo "\n Original str =$@"
    for i in "$@"; do
        [[ $i ]] && tmp_array["${i:- }"]='.'
        #[[ $i ]] && IFS=" " tmp_array["${i:- }"]=1		

	echo "'i:-:' ${i:-}"
    echo ".. tmp_array str =${tmp_array[@]}"
	echo ".. ! tmp_array str =${!tmp_array[@]}"
	echo " "
    done
	
    printf '%s ' "${!tmp_array[@]}"
}

echo "remove_array_dups z hh ff 66 6 66 5 5 5"
remove_array_dups z hh ff 66 6 66 5 5 5

