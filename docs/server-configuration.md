---
title: Server Configuration
sidebar_label: Server Configuration
sidebar_position: 3
---

# Server Configuration for WordPress Optimization

This section covers the server setup required for a high-performance WordPress environment. We'll use **CyberPanel**, **OpenLiteSpeed**, **MariaDB**, and **PHP (LSAPI)** to create a robust and scalable hosting stack.

## Prerequisites

- **Ubuntu 22.04 LTS** (CyberPanel does not yet support Ubuntu 24.04).
- A fresh server with root access.

Update your system and install essential tools:

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y curl wget git unzip
```


## 1. Install CyberPanel

CyberPanel is a powerful control panel that simplifies server management. Install it with the following command:

```bash
sh <(curl https://cyberpanel.net/install.sh || wget -O - https://cyberpanel.net/install.sh)
```

### Installation Options

- **Type**: Full installation
- **Web Server**: OpenLiteSpeed
- **Remote MySQL**: No
- **Install Memcached and Redis**: No (LSCache handles caching)
- **Install WatchDog**: Yes
- **Admin Email**: Set your email
- **Admin Password**: Set your password

### Access CyberPanel

- **URL**: `https://<your-server-ip>:8090`
- **Username**: `admin`
- **Password**: `<your-password>`



## 2. Configure OpenLiteSpeed

OpenLiteSpeed is a lightweight, high-performance web server. Configure the admin password:

```bash
/usr/local/lsws/admin/misc/admpass.sh
```

### Access OpenLiteSpeed Admin

- **URL**: `https://<your-server-ip>:7080`
- **Username**: `admin`
- **Password**: `<your-password>`


## 3. Install and Configure MariaDB

MariaDB is a reliable, high-performance database server. Install it with:

```bash
sudo apt install mariadb-server mariadb-client -y
```

### Retrieve MariaDB Root Password

You can find the root password in the CyberPanel configuration file:

```bash
cat /etc/cyberpanel/mysqlPassword
```

### Optimize MariaDB for WordPress

Edit the MariaDB configuration file:

```bash
sudo nano /etc/mysql/mariadb.conf.d/50-server.cnf
```

Add or adjust the following settings:

```ini
[mysqld]
# InnoDB settings
innodb_buffer_pool_size = 2G         # Adjust to ~70% of available RAM
innodb_log_file_size = 256M          # Good for write-heavy workloads
innodb_flush_log_at_trx_commit = 1   # Better performance with slight durability trade-off
innodb_flush_method = O_DIRECT       # Bypass OS cache for better stability

# Query settings
query_cache_type = 0                 # Disable query cache (better for WordPress)
query_cache_size = 0                 # Disable completely
join_buffer_size = 1M                # Help with complex joins
sort_buffer_size = 2M                # Improve sorting performance
read_buffer_size = 2M
read_rnd_buffer_size = 1M

# Connection and cache settings
max_connections = 200                # Good baseline for most sites
thread_cache_size = 50               # Reduce connection overhead
table_open_cache = 400               # WordPress uses many tables
table_definition_cache = 2000        # Cache table definitions
open_files_limit = 65535             # Prevent "too many open files" errors

# Logging (minimal for performance)
slow_query_log = 1
slow_query_log_file = /var/log/mysql/mariadb-slow.log
long_query_time = 2
```

Restart MariaDB:

```bash
sudo systemctl restart mariadb
```



## 4. PHP Configuration (LSAPI with OPcache)

Optimize PHP for WordPress by editing the PHP configuration in CyberPanel:

1. Go to **CyberPanel → PHP → Edit PHP Configs → 8.1**.
2. Add the following settings to the end of the file:

```ini
; PHP Memory Settings
memory_limit = 1024M
max_execution_time = 300
max_input_time = 300
post_max_size = 128M
upload_max_filesize = 128M
max_input_vars = 5000
file_uploads = On

; Error Handling - Disable for production
error_reporting = E_ALL & ~E_DEPRECATED & ~E_STRICT
display_errors = Off
display_startup_errors = Off
log_errors = On
error_log = /var/log/php_errors.log

; Performance Optimizations
realpath_cache_size = 4M
realpath_cache_ttl = 120

; OPcache Settings - Aggressive Performance
[opcache]
zend_extension=opcache
opcache.enable = 1
opcache.enable_cli = 1
opcache.memory_consumption = 512
opcache.interned_strings_buffer = 64
opcache.max_accelerated_files = 32531
opcache.max_wasted_percentage = 5
opcache.use_cwd = 0
opcache.validate_timestamps = 0
opcache.revalidate_freq = 0
opcache.save_comments = 1
opcache.fast_shutdown = 1
opcache.consistency_checks = 0
opcache.optimization_level = 0xffffffff

; OPcache JIT Settings (PHP 8+)
opcache.jit = 1255
opcache.jit_buffer_size = 256M

; File Handling
allow_url_fopen = On
allow_url_include = Off

; Session Settings
session.save_handler = files
session.save_path = "/var/lib/php/sessions"
session.use_strict_mode = 1
session.use_cookies = 1
session.cookie_secure = 1
session.use_only_cookies = 1
session.name = PHPSESSID
session.cookie_lifetime = 0
session.cookie_path = /
session.cookie_domain =
session.cookie_httponly = 1
session.gc_maxlifetime = 1440
session.gc_probability = 1
session.gc_divisor = 100
session.cache_expire = 180
session.cache_limiter = nocache
session.sid_length = 48
session.sid_bits_per_character = 6
session.lazy_write = 0

; Date Settings
date.timezone = UTC

; MySQL/MariaDB Settings
mysqlnd.collect_memory_statistics = Off

; Zlib Output Compression
zlib.output_compression = On
zlib.output_compression_level = 9

; LSAPI Specific Settings
lsapi.use_output_buffering = On
lsapi.allow_persistent_connections = On
lsapi.backend_accept_once = Off
lsapi.socket_owner = nobody
lsapi.socket_group = nobody
lsapi.socket_mode = 0660
lsapi.max_process_time = 300
lsapi.memory_limit = 1024M
lsapi.children_start_request = 5
```

3. Restart PHP using the button in CyberPanel.


## Next Steps

With the server configured, you're ready to install and optimize WordPress. Proceed to the next section to learn how to set up WordPress for **Core Web Vitals** and **SEO**.

