---
layout: post
comments: true
categories: GEM5 CPU2006 

---

SPEC CPU 2006��һ���Ƚ��ϵ�benchmark�������ڽ��µ�Linuxϵͳ�ϱ������ֲ����ݵ����⡣�ڱ�������У���Ҫ��SPEC CPU 2006��Դ�����������޸��������µ�Linuxϵͳ��������CentOS 7ϵͳΪ����������Linuxϵͳ��SPEC CPU 2006�ı�����̡�

#### Compile

���ȣ����ڼ���������SPEC CPU 2006���Դ���install.sh�ļ������в��˵ģ�������Ҫ���±���Դ���롣���� './tool/src' Ŀ¼������buildtools�ļ���

    ./buildtools

#### Debug
	
���й����У�����ּ������������г��⼸���������Ӧ�Ľ��������

1. error building specmd5sum

    ����specmd5sumʱ����������´���
    
	    gcc -DHAVE_CONFIG_H    -I/home/gem5/cpu2006/tools/output/include   -I. -Ilib  -c -o md5sum.o md5sum.c
        In file included from md5sum.c:38:0:
        lib/getline.h:31:1: error: conflicting types for 'getline'
         getline PARAMS ((char **_lineptr, size_t *_n, FILE *_stream));
         ^
        In file included from md5sum.c:26:0:
        /usr/include/stdio.h:678:20: note: previous declaration of 'getline' was here
         extern _IO_ssize_t getline (char **__restrict __lineptr,
                    ^
        In file included from md5sum.c:38:0:
        lib/getline.h:34:1: error: conflicting types for 'getdelim'
         getdelim PARAMS ((char **_lineptr, size_t *_n, int _delimiter, FILE *_stream));
         ^
        In file included from md5sum.c:26:0:
        /usr/include/stdio.h:668:20: note: previous declaration of 'getdelim' was here
          extern _IO_ssize_t getdelim (char **__restrict __lineptr,
                             ^
        make: *** [md5sum.o] Error 1
        + testordie 'error building specmd5sum'
        + test 2 -ne 0
        + echo '!!! error building specmd5sum'
        !!! error building specmd5sum
        + kill -TERM 1299
        + exit 1
        !!!!! buildtools killed
		
	����ԭ����Ҫ����Ϊ������ͻ��stdio.h���Ѿ�����getline��getdelim��������SPEC CPU 2006�е�getline.h��Ҳ������������������
	
	�����������/tools/src/specmd5sum/md5sum.c�ļ���ע�͵�getline.hͷ�ļ�����25�У�
	    
		//#include "getline.h"
		
2. error building Perl

        ����Perlʱ�������������������
        
		collect2: error: ld returned 1 exit status
        make: *** [miniperl] Error 1
        + testordie 'error building Perl'
        + test 2 -ne 0
        + echo '!!! error building Perl'
        !!! error building Perl
        + kill -TERM 15173
        + exit 1
        !!!!! buildtools killed
		
		t/op/sprintf..............................FAILED--no leader found
        t/op/sprintf2.............................FAILED--expected 263 tests, saw 3
		
	����ԭ��1) �߰汾��Linux�ں���ɾ����asm/page.hͷ�ļ�; 2) ����perlʱ����Ҫ�õ���ѧ��;
	
	���������
	1) ��tools/src/perl-5.8.8/ext/IPC/SysV/SysV.xs�ļ���ע��asm/page.hͷ�ļ�����7�У�
	
	    //#   include <asm/page.h>
	
	2) ��/tools/src/buildtools�ļ����ڱ���perl���벿�֣���333�к�334�У��������޸ģ�
	�޸�ǰ��
	
	    LD_LIBRARY_PATH=`pwd`
        DYLD_LIBRARY_PATH=`pwd`
        export LD_LIBRARY_PATH DYLD_LIBRARY_PATH
        ./Configure -dOes -Ud_flock $PERLFLAGS -Ddosuid=undef -Dprefix=$INSTALLDIR -Dd_bincompat3=undef -A ldflags=-L${INSTALLDIR}/lib -A ccflags=-I${INSTALLDIR}/include -Ui_db -Ui_gdbm -Ui_ndbm -Ui_dbm -Uuse5005threads ; testordie "error configuring perl"

    �޸ĺ�
	
        LD_LIBRARY_PATH=`pwd`
        DYLD_LIBRARY_PATH=`pwd`
        ./Configure -Dcc="gcc -lm" -Dlibpth='/usr/local/lib64 /lib64 /usr/lib64' -dOes -Ud_flock $PERLFLAGS -Ddosuid=undef -Dprefix=$INSTALLDIR -Dd_bincompat3=undef -A ldflags=-L${INSTALLDIR}/lib -A ccflags=-I${INSTALLDIR}/include -Ui_db -Ui_gdbm -Ui_ndbm -Ui_dbm -Uuse5005threads ; testordie "error configuring perl"	

	
	
	
	
	
	