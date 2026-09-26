# VPN_Proxy_Routing on Fedora 44 Konsole
# Terminal Alias for proxy ON & OFF

how to use:
in terminal type `proxy_on` will result in
```bash

[✔] Terminal proxy routing enabled (127.0.0.1:7897)
```


type `proxy_status` will result in 
```bash

Current Proxy Configuration:  
----------------------------  
http_proxy  = http://127.0.0.1:7897  
https_proxy = http://127.0.0.1:7897  
all_proxy   = socks5h://127.0.0.1:7897
```


type `proxy_off` will result in 
```bash
proxy_off  
[✘] Terminal proxy routing disabled
```


This is the script I write to` ~/.bashrc` to toggle proxy on or off
```bash
cat << 'EOF' >> ~/.bashrc

# --- Proxy Toggles for Clash Mixed Port ---
proxy_on() {
    export http_proxy="http://127.0.0.1:7897"
    export https_proxy="http://127.0.0.1:7897"
    export HTTP_PROXY="http://127.0.0.1:7897"
    export HTTPS_PROXY="http://127.0.0.1:7897"
    export all_proxy="socks5h://127.0.0.1:7897"
    export ALL_PROXY="socks5h://127.0.0.1:7897"
    alias sudo='sudo -E '
    echo -e "\e[1;32m[✔] Terminal proxy routing enabled (127.0.0.1:7897) sudo -E enabled\e[0m"
}

proxy_off() {
    unset http_proxy https_proxy HTTP_PROXY HTTPS_PROXY all_proxy ALL_PROXY
    unalias sudo 2>/dev/null
    echo -e "\e[1;31m[✘] Terminal proxy routing disabled. sudo -E disabled\e[0m"
}

# Optional status check shortcut
proxy_status() {
    echo "Current Proxy Configuration:"
    echo "----------------------------"
    echo "http_proxy  = $http_proxy"
    echo "https_proxy = $https_proxy"
    echo "all_proxy   = $all_proxy"
}
EOF


```
