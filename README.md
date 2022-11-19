# Aux_Project
>>### Shell Script to automate onboarding of new users on a linux server  

### Different codes used in the project:
1. #### This command locks the script to ensure only a user with sudo priviledge can run it
    if [ $(id -u) -eq 0 ]; then

2. #### creating a loop to read the names stored in the userfile(names.csv)
        for user in $NEW_USERS;
        do
            echo $user 
            if id "$user" &>/dev/null
             then 
             echo "user exists"else

3. ### This command will create a new user 
    useradd -m -d /home/$user \
            -s /bin/bash \
            -g developers $user 
    echo "New User Created"

4. ### This command will create a ssh and home directory for the users 
    echo 

    su - -c "mkdir ~/.ssh" $user
    echo ".ssh and home folder successfully created for new user "

5. ### This command will set permissions for the key_file
    echo
    
    su - -c "chmod 700 ~/.ssh" $user
    echo "directory Permission set for created user"

6. ### This command will create an authorized_key_file 
    echo 

    su - -c "touch ~/.ssh/authorized_keys" $user
    echo "authorized_keys directly successfully created"

7. ### This command will set permission for the authorized_key file 
    echo 

    su - -c "chmod 600 ~/.ssh/authorized_keys" $user
    echo "Permission set successfully for authorized_keys file"

8. ### This command will set public key for the users in the server 
    cp -R "/root/onboard/id_rsa.pub" "/home/$user/.ssh/authorized_keys"

    echo "public key file successfully copied to user account on the server"

    echo "User Successfully Created"

9. ### Generating a Password for users 
    sudo echo -e "teejay\nteejay" | sudo passwd "$user"
    
    sudo passwd -x 7 $user
    
    fi 
    
            done
    
    else
    
    echo "only Admin can onboard a User"
    
    fi

10. ### Making Directory for Script **(mkdir shell)**
![Making Directory for script](Making%20Shell%20Directory%20and%20Going%20into%20it.png)


11. ### Creating CSV file in Shell directory **(touch names.csv)**

![Creating csv file](/Creating%20names.csv%20file%20and%20updating%20it.png)

12. ### Populating csv file with random names

![Populating names.csv](/Populating%20names.scv%20file.png)

13. ### Creating developers group on server **(Sudo groupadd developers)**

![](Creating%20Developers%20group.png)

14. ### Creating directory for public key & Private key and populating it with public key **(mkdir id_rsa.pub id_rsa)**

![](creating%20Keys%20Directory.png)

![](Populating%20Public%20key%20id_rsa.pub.png)

![](Populating%20Private%20key%20file%20id_rsa.png)

15. ### Running the script **(./onboarding.sh)**

![](Running%20the%20script%2C%20users%20being%20created%20successfully.png)

16. ### users successfully created

![](20%20new%20users%20successfully%20created.png)

17. ### Logged in as another user (Kunle) and verifyying .ssh folder is created including home directory 

![](Logged%20in%20as%20Kunle%20.ssh%20folder%20present.png)

