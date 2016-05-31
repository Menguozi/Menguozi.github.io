---
layout: post
comments: true
categories: PARSEC

---
> ### Download

Download parsec-3.0 from its [official website](http://parsec.cs.princeton.edu/download.htm).

> ### Compile

Uncompress the parsec-3.0 compressed file, and compile it using the following instruct:

    sudo ./bin/parsecmgmt -a build
	
> ### Debug

1) Error 1: pod2man error

    POD document had syntax errors at /usr/bin/pod2man line 69.  
    make: *** [install_docs] Error 1   
    [PARSEC] Error: 'env PATH=/usr/bin:/home/gem5/parsec-3.0/bin:/sbin:/bin:/usr/sbin:/usr/bin /usr/bin/make install' failed.   
	
  Solution: delete pod2man file
  
      sudo rm /usr/bin/pod2man
	  
2) Error 2: 
  


