## Steps to configure and setup vagrant provisioning to automate pushing a zipped file

1. Pick a fedora image

    ```bash
    vagrant init jacobw/fedora35-arm64
    ```

2. Set the public and private network

3. Set the ram size needed for the server

4. Add your provisioning script from the manual setup and then check the result on the IP

   ```bash
    yum install wget httpd unzip -y

    systemctl start httpd

    systemctl enable httpd

    systemctl stop firewalld

    systemctl disable firewalld

    mkdir -p /tmp/finance

    cd /tmp/finance/

    wget https://www.tooplate.com/zip-templates/2135_mini_finance.zip

    unzip -o 2135_mini_finance.zip

    cp -r 2135_mini_finance/* /var/www/html

    systemctl restart httpd

    cd /tmp/
    
    rm -rf /tmp/finance
    ```

   explanation:

    * install packages
    * start httpd service
    * set httpd service to auto-start from boot-time
    * stop firewall service
    * disable boot-time load for firewall service
    * make a finance folder in the tmp director (`-p` make sure that this code does not fail when the folder already exit)
    * enter the finance folder
    * download the zipped website
    * unzip the website (`-o` to overwrite previously written files)
    * move the files unzipped to the `/var/www/html` folder
    * restart httpd service
    * leave the finance folder
    * delete the finance folder
