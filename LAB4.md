### **Lab Outline**

1. **Prerequisites**
2. **Volumes**
3. **Bind Mounts**
4. **Tmpfs Mounts**

### **Prerequisites**

- Docker installed on your system.
- Basic understanding of Docker commands.

### **Step 1: Volumes**

Volumes are managed by Docker and are the preferred mechanism for persisting data in Docker containers.

### **Create and Use Volumes**

1. **Create a Volume:**
    
    ```
    docker volume create my_volume
    ```
    
2. **Run a Container with a Volume:**
    
    ```
    docker run -d -v my_volume:/data --name volume_container ngin
    ```
    
    This command runs an Nginx container and mounts the **`my_volume`** volume to the **`/data`** directory in the container.
    
3. **Write Data to the Volume:**
    - Access the container:
        
        ```
        docker exec -it volume_container /bin/bash
        ```
        
    - Write data to the volume:
        
        ```
        echo "Hello, Docker Volume!" > /data/hello.txt
        exit
        ```
        
4. **Verify Data Persistence:**
    - Stop and remove the container:
        
        ```
        docker stop volume_container
        docker rm volume_container
        ```
        
    - Run a new container with the same volume:
        
        ```
        docker run -d -v my_volume:/data --name new_volume_container nginx
        docker exec -it new_volume_container /bin/bash
        cat /data/hello.txt
        ```
        
    
    You should see the content "Hello, Docker Volume!" confirming that the data persisted.
    

### **Step 2: Bind Mounts**

Bind mounts map a directory or file from the host filesystem into a container.

### **Create and Use Bind Mounts**

1. **Create a Directory on the Host:**
    
    ```
    mkdir /tmp/my_bind_mount
    ```
    
2. **Run a Container with a Bind Mount:**
    
    ```
    docker run -d -v /tmp/my_bind_mount:/data --name bind_mount_container nginx
    ```
    
3. **Write Data to the Bind Mount:**
    - Access the container:
        
        ```
        docker exec -it bind_mount_container /bin/bash
        ```
        
    - Write data to the bind mount:
        
        ```
        echo "Hello, Bind Mount!" > /data/hello.txt
        exit
        ```
        
4. **Verify Data on Host:**
    
    ```
    cat /tmp/my_bind_mount/hello.txt
    ```
    
    You should see the content "Hello, Bind Mount!" confirming that the data is shared between the host and the container.
    

### **Step 3: Tmpfs Mounts**

Tmpfs mounts are temporary filesystems stored in the host's memory (RAM).

### **Create and Use Tmpfs Mounts**

1. **Run a Container with a Tmpfs Mount:**
    
    ```
    shCopy code
    docker run -d --tmpfs /data:rw,noexec,nosuid,size=64m --name tmpfs_mount_container nginx
    ```
    
2. **Write Data to the Tmpfs Mount:**
    - Access the container:
        
        ```
        docker exec -it tmpfs_mount_container /bin/bash
        ```
        
    - Write data to the tmpfs mount:
        
        ```
        echo "Hello, Tmpfs Mount!" > /data/hello.txt
        exit
        ```
        
3. **Verify Data Persistence:**
    - Stop and remove the container:
        
        ```
        docker stop tmpfs_mount_container
        docker rm tmpfs_mount_container
        ```
        
    - Run a new container with the same tmpfs mount:
        
        ```
        docker run -d --tmpfs /data:rw,noexec,nosuid,size=64m --name new_tmpfs_mount_container nginx
        docker exec -it new_tmpfs_mount_container /bin/bash
        ls /data
        ```
        
    
    The file will not be there, confirming that the data was ephemeral.

   CLI Cheetsheet -> https://dockerlabs.collabnix.com/intermediate/docker-compose/#cli-cheatsheet 
