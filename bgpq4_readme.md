## bgpq4 Readme

### What is  `bgpq4`

> bgpq4 eases BGP filter maintenance by automatically generating prefix lists, (extended) access lists, policy statement terms and AS-path lists using IRR routing data. It features IPv6 prefix-/access-list support, aggregation of generated filters and output compatible with Cisco, Juniper, Mikrotik, Nokia, OpenBGPD and BIRD.

### Installing BGPQ4 on Various Operating Systems:

**1. macOS:**

-   Install Homebrew package manager (if not already installed):
    ```bash
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    ```
    
-   Install BGPQ4 using Homebrew:
    
       ```bash
       brew install bgpq4
       ```
**2. Ubuntu / Debian-based Linux:**

-   Update the package index:
    ```bash
    sudo apt update
    ```
-   Install BGPQ4:
    ```bash
    sudo apt -y install bgpq4
    ```
**3. CentOS / RHEL-based Linux:**

-   Enable the Extra Packages for Enterprise Linux (EPEL) repository (if not enabled):
   ```bash
   sudo yum install epel-release
```
-   Install BGPQ4:
    ```bash
    sudo yum install bgpq4
    ```

**4. FreeBSD:**

-   Install BGPQ4 using the FreeBSD package manager:
  
    ```bash
    sudo pkg install bgpq4
    ```

**5. OpenBSD:**

-   Install BGPQ4 using the OpenBSD package manager:
    
    `doas pkg_add bgpq4` 
    

**6. NetBSD:**

-   Install BGPQ4 using the NetBSD package manager:
    
    ```bash
    pkgin install bgpq4 
    ```
**7. Other Unix-like Systems:**

-   Download the source code from the official BGPQ4 repository:
      ```bash
    git clone https://github.com/bgp/bgpq4.git 
    ```
-   Navigate to the downloaded directory:
      ```bash
    cd bgpq4
    ```
-   Compile and install BGPQ4:
      ```bash
    make
    sudo make install
	```

## EXAMPLES

### Juniper  
IPv4 exact-match filter from AS-SET
```
$ bgpq4 -Jl AS23918-exact-in AS23918:AS-GLOBAL
policy-options {
replace:
prefix-list AS23918-exact-in {
.....
 }
}
```
IPv6 exact-match filter from AS-SET
```
$ bgpq4 -J6l AS23918v6-exact-in AS23918:AS-GLOBAL
policy-options {
replace:
prefix-list AS23918v6-exact-in {
.....
 }
}
```
### Cisco
For Cisco we can use aggregation (-A) flag to make this prefix-filter more compact:

ipv4 exact-match filter from AS-SET
```
$ bgpq4 -Al AS23918-in AS23918:AS-GLOBAL
no ip prefix-list AS23918-in
ip prefix-list AS23918-in permit 5.187.16.0/20
....
```

ipv4 exact-match filter from AS-SET

```
$ bgpq4 -A6l AS23918v6-in AS23918:AS-GLOBAL
no ipv6 prefix-list AS23918v6-in
ipv6 prefix-list AS23918v6-in permit 2401:4700:3000::/48
....

## bgpq4 github page:

[https://github.com/bgp/bgpq4](https://github.com/bgp/bgpq4)

