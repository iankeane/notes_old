Ian Keane  

--------  
Networks  
--------  


Mon Jan 11 02:36:43 EST 2016  
-------------------------------------------------  

login:yd9  
passwd:64jdE35v  
ports:22400-22499  

Network Protocols  
    a protocol is a set of rules governing communication  
        ex: the person who recieves a phone call speaks first  
        the caller then identifies himself  
    protocols have to be well defined  
        if protocols are well defined and agreed upon, the server and client  
            can be written separately (or in different languages)  
        protocols are created by Internet Engineering Task Force  
        protocols are called RFC's (request for comment)  

Layered Protocol Model  
    application layer  
        services specific to application being used  
        ex: HTTP, FTP, SSH, SMTP  
        implemented in application code  
        app-specific message  
    transport layer  
        ex: TCP, UDP  
        application code never goes deeper than transport layer  
        delivers to a process on a host  
        implemented in OS code  
        messagees are called segment or datagrams  
    network layer  
        ex: IP, ICMP, IGMP  
        delivers to a remote host  
        implemented in OS  
    data link  
        ex: ethernet, X.25, ARP, NDP  
        delivery to directly connected host  
        implimented in hardware  

Protocol Layering Principle  
    a principle is a guideline used by designers  
        each principle uses the protocol of the layer below it  
    you only need to understand the services of the layer being used (not the  
        ones below it)  
    only need to know the services of the lower layer  
    first assignment is to write an application layer protocol using  
        a transportation layer protocol  

OSI Layer 7 Model  
    we will only use this for the layer numbers  
    !!! Numbers go here  

Network Service Daemon  
    metaphor for a sorcerer conjuring a demon (demon already exists)  
    a daemon is a process that recieves messages  
    daemons are only needed when someone wants to recieve and send a message  
    held by OS in sleep, awakened by hardware interrupt (analogous to phone  
        ring)  

Morris Internet Worm (1988)  
    exploited vulnerabilities in daemons for rsh, finger, sendmail  
    unintentional worm, shut down entire internet  

Network Performance Measures  
    bandwidth (bits per second on a specific link)  
    transmission delay  
    propagation delay  
    queueing delay  
    traffic intensity  
    bit error rate  
    packet loss rate  
    together, these make up the quality of service measure  


Tue Jan 12 14:05:16 EST 2016  
-------------------------------------------------  

Sockets  
    every program has an abstraction called a socket  
        metaphor for an electrical plug  
        "system hook" into tranport layer services  
    they are at the boundary between the application/transport layes  
    sockets do nothing if not connected  
    two types of socket  
        UDP (unreliable)  
        TCP  
    tradeoff between reliablity and speed  
    TCP takes slightly longer to close a socket  
    there are two sides to a socket  
        sending side  
        recieving side  
            recieving side must start listening before a message arrives  
    in a socket's final state, it is a connection  
       a socket connection is a two-way data pipe  

Process Scheduling  
    ps -ef lists all processes of all users on system  
    process states:  
        running when the cpu is executing its instructions  
        suspended when the cpu is running some other process  
        blocked when it cannot run because it must wait for resources  
    processes are scheduled on queues  
        "ready" and "waiting" queue  
        they are removed from the ready queue after a "timeslice"  
        a process "looses its timeslice" after a set time, and is set back on  
            the waiting queue  
    process waiting for a message that will never come is a "zombie"  
    socket life cycle  
        created  
        -> listening  
        -> BLOCKED  
        -> suspended(wait queue)  
        -> ready queue  
        -> runs, recieves data  
        -> destroyed  

Ports  
    a port is like a local address  
    multiplexing is when multiple communications take place along the same  
        channel  
    demultiplexing is breaking down which communications come from where  
    

Thu Jan 14 14:06:05 EST 2016  
----------------------------  

Methodologies  
    waterfall  
        steps:  
            requirements  
            -> design  
            -> implementation  
            -> verification  
            -> maintenance  
        causes communication problems  
    agile programming  
        each iteration adds functionality  
        automated unit testing protects against bugs  
        refactoring takes place if necessary  
    TDD process:  
        1. Break project into classes  
        2. Define task of each class  
        3. Test code specifies specific operation results  
        4. Make the test pass  
        5. Improve test by refactoring  
        6. Move on to next iteration  
    sample iterations:  
        Iteration 1: 
            simple entity class  
                only holds data  
            test classes  
                test basic function of entity classes  
        Iteration 2:  
            encode a list of items  
                encoding is preparation to send something across a network  
                can be done by serialization as well  
            put todo stubs in code skeleton  

Exercise  
    find.py (from python exercises)  
        find . -name sunny\*  
            find file with name starting with sunny in current dir  
        search files recursively  
            recursion is not hard if task is identified  
        task: search a folder and all its subfolders for pattern  
            only name criteria is required for this project  
        find(dir,query)  
            search current folder files  
            call find(name) on target directory  
            if match, return  
    make a main  
    import sys  
        use readArgs() to get arguments  
        loop: for arg in sys.argv  
            arg does not need to be declared beforehand  
            0th argument is always the name of the python file  
    guidelines  
        1. meaningful variable names  
        2. loop comments  
        3. method specs  


Tue Jan 19 14:03:13 EST 2016  
----------------------------  

HTTP and TCP  
    network traffic requires numeric ip address  
    DNS - Domain Naming Service  
        first thing invoked is DNS  
        takes the domain name and returns ip  
    persistent TCP connection:  
        1. Server starts and listens (passive open)  
        2. Client initiates TCP request (active open)  
        3. Server and client complete three way handshake (transport level)  
            (connection is now open) (request-response protocol)  
            1. First client request  
            2. First server response  
            3. Second client request  
            3. second server response  
            4. ...  
        4. Server times out and closes connection  
    a HTTP request is a stream of ASCII characters broken into lines  
        delevered to a well-known TCP port (80 or 8080)  
            80 and 8080 are always used  
                80 is generally an apache server  
                8080 is generally a java server  
        uses name-value syntax  
                has a header with name value pairs (called response codes), one per line  
                uses RFC 2616  
            response codes use backus-naur form  
            there are other types of headers, such as entity and extension  
                headers  
    HTTP request methods  
        a method is safe if it does not change data on the server  
            a GET method should be safe  
        a method is idempotent if making a request N times has the same effect  
            as making the request once  
            GET, PUT, and DELETE are idempotent  
        POST method  
    Cookies  
        a cookie is a small piece of info attatched to a website  
            used for logins and targeted advertizing  
        the cookies that are most important are the ones that are sent back to  
            the machine they came from  
            these are used to maintain login info  
        cookies are opt-out  
        session ID is established on login  
            must be encrypted, as it can be used to steal your session  
    Content Negotiation  
        user agent may present these headers to the server:  
            Accept  
            Accept-Charset  
            Accept-Encoding  
            Accept-Language  
            User-Agent  
        used to control things like language  
    Caching  
        a cache is a temporary storage area  
            sends a saved copy of a page instead of reloading the same request  
            usually has some kind of timeout  
            controlled using cache control headers  
        caching is used for static content, not dynamic  

FTP  
    a stateful protocol  
    uses two connections:  
        control connection  
            sends commands  
        data connection  
            controls data?  


Common Gateway Interface  
    allows us to put variales in the url  
        GET method: embed vars in URL  
        POST Method: open separate input stream  

