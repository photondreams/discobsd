TOPSRC!=cd ../../..; pwd
include ${TOPSRC}/share/mk/sys.mk

# Favor assembler source files over their C source equivalent.
.SUFFIXES:
.SUFFIXES: .o .S .c

LIBCDIR          = $(TOPSRC)/lib/libc

.PATH:	${LIBCDIR}/${MACHINE_ARCH}/sys ${LIBCDIR}/${MACHINE_ARCH}/string \
	${LIBCDIR}/${MACHINE_ARCH}/gen ${LIBCDIR}/gen ${LIBCDIR}/stdio \
	${LIBCDIR}/stdlib ${LIBCDIR}/string ${LIBCDIR}/inet \
	${LIBCDIR}/compat ${LIBCDIR}/runtime

VPATH=	${LIBCDIR}/${MACHINE_ARCH}/sys ${LIBCDIR}/${MACHINE_ARCH}/string \
	${LIBCDIR}/${MACHINE_ARCH}/gen ${LIBCDIR}/gen ${LIBCDIR}/stdio \
	${LIBCDIR}/stdlib ${LIBCDIR}/string ${LIBCDIR}/inet \
	${LIBCDIR}/compat ${LIBCDIR}/runtime

COPTS!=if [ x"${MACHINE_ARCH}" = x"mips" ] ; then \
		echo "-Wa,-x -B${TOOLBINDIR}/" ; \
	else \
		echo "" ; \
	fi

ASOPTS!=if [ x"${MACHINE_ARCH}" = x"mips" ] ; then \
		echo "-Wa,-x -B${TOOLBINDIR}/ -DLWHI=lwr -DLWLO=lwl -DSWHI=swr -DSWLO=swl" ; \
	else \
		echo "" ; \
	fi

DEFS		= -Wall -ffreestanding
CFLAGS		= ${DEFS} -Os -Wno-attributes -Wno-attribute-alias ${COPTS}
ASFLAGS		= ${DEFS} -I${LIBCDIR}/${MACHINE_ARCH}/sys ${ASOPTS}

# modules which can not use SYSCALL and must be assembled from sources.  The
# rest of the system calls are generated with printf(1) and do not have
# source files associated with them.

# libc/$(MACHINE_ARCH)/sys
SYSOBJS		= __sysctl.o accept.o access.o adjtime.o bind.o chdir.o \
		  chflags.o chmod.o chown.o chroot.o close.o connect.o dup.o \
		  dup2.o execve.o fchdir.o fchflags.o fchmod.o fchown.o \
		  fcntl.o flock.o fork.o fstat.o fsync.o ftruncate.o \
		  getdtablesize.o getgroups.o getitimer.o getsockname.o \
		  getpeername.o getpriority.o getrlimit.o getrusage.o \
                  getsockopt.o gettimeofday.o ioctl.o kill.o killpg.o link.o \
                  listen.o lstat.o mkdir.o mknod.o mount.o open.o pselect.o \
                  quota.o read.o readlink.o readv.o reboot.o recv.o \
                  recvfrom.o recvmsg.o rename.o rmdir.o select.o send.o \
                  sendmsg.o sendto.o setgroups.o setitimer.o setpgrp.o \
                  setpriority.o setquota.o setuid.o seteuid.o setgid.o \
                  setegid.o setrlimit.o setsockopt.o settimeofday.o \
                  shutdown.o sigaltstack.o socket.o socketpair.o stat.o \
                  symlink.o sigprocmask.o sigstack.o sigwait.o statfs.o \
                  fstatfs.o getfsstat.o truncate.o umount.o unlink.o \
                  utimes.o wait4.o write.o writev.o lseek.o sigsuspend.o \
		  getgid.o getegid.o getpgrp.o getpid.o getppid.o getuid.o \
                  geteuid.o profil.o sigpending.o sync.o ufetch.o ustore.o \
                  ucall.o umask.o vfork.o vhangup.o rdglob.o wrglob.o

OBJS		= $(SYSOBJS) sbrk.o execl.o execle.o execv.o \
		  _exit.o _brk.o pipe.o ptrace.o sigaction.o

# libc/$(MACHINE_ARCH)/string
OBJS            += bcopy.o bzero.o ffs.o memcpy.o memmove.o memset.o \
                   strlen.o bcmp.o index.o rindex.o strcmp.o

# libc/$(MACHINE_ARCH)/gen
OBJS            += _setjmp.o htonl.o htons.o

# libc/gen
OBJS            += abort.o alarm.o atof.o atoi.o atol.o basename.o \
                   calloc.o closedir.o crypt.o ctime.o ctype_.o \
                   daemon.o devname.o dirname.o ecvt.o err.o \
                   execvp.o fakcu.o frexp.o fstab.o gcvt.o getenv.o getgrent.o \
                   getgrgid.o getgrnam.o getlogin.o \
                   getgrouplist.o gethostname.o getpagesize.o \
                   getpass.o getpwent.o getloadavg.o getmntinfo.o \
                   getttyent.o getttynam.o getusershell.o getwd.o \
                   initgroups.o isatty.o isinff.o isnanf.o ldexp.o malloc.o mktemp.o \
                   modff.o ndbm.o nlist.o knlist.o opendir.o perror.o popen.o \
                   psignal.o qsort.o random.o readdir.o regex.o scandir.o \
                   seekdir.o setmode.o sethostname.o setenv.o siglist.o \
                   signal.o siginterrupt.o sigsetops.o \
                   sleep.o strcasecmp.o strftime.o swab.o sysctl.o syslog.o system.o \
                   strcat.o strncat.o strcpy.o strncpy.o strncmp.o \
                   telldir.o time.o timezone.o ttyname.o ttyslot.o ualarm.o usleep.o \
                   strdup.o uname.o wait.o wait3.o waitpid.o

# libc/stdio
OBJS            += fgetc.o fgets.o fputc.o fputs.o gets.o puts.o \
                   clrerr.o doscan.o exit.o fdopen.o filbuf.o findiop.o \
                   flsbuf.o fopen.o fprintf.o fread.o freopen.o fseek.o \
                   ftell.o fwrite.o getchar.o getw.o printf.o putchar.o putw.o \
                   rew.o scanf.o setbuf.o setbuffer.o setvbuf.o snprintf.o sprintf.o \
                   strout.o ungetc.o vfprintf.o vprintf.o vsprintf.o doprnt.o \
                   remove.o feof.o ferror.o fileno.o

# libc/stdlib
OBJS            += getopt.o getsubopt.o strtol.o strtoul.o strtod.o

# libc/string
OBJS            += strcspn.o strerror.o strlcat.o strlcpy.o strpbrk.o \
                   strsep.o strspn.o strstr.o strtok.o strtok_r.o

# libc/inet
OBJS            += inet_addr.o inet_network.o inet_netof.o \
                   inet_ntoa.o inet_lnaof.o inet_maddr.o

# libc/compat
OBJS            += creat.o ftime.o gethostid.o memccpy.o memchr.o \
                   memcmp.o memcpy.o memset.o nice.o pause.o rand.o \
                   sethostid.o setregid.o setreuid.o setrgid.o setruid.o \
                   sigcompat.o strchr.o strrchr.o times.o tmpnam.o \
                   utime.o

# libc/runtime
OBJS+=		addsf3.o comparesf2.o divsf3.o fixsfsi.o fixunssfsi.o \
		floatsisf.o floatunsisf.o mulsf3.o negsf2.o subsf3.o \
		adddf3.o comparedf2.o divdf3.o fixdfsi.o fixunsdfsi.o \
		floatsidf.o floatunsidf.o muldf3.o negdf2.o subdf3.o \
		ashldi3.o lshrdi3.o \
		sc_case.o

all:            ../libc.a

../libc.a:	${OBJS}
		rm -f $@
		${AOUT_AR} rc $@ ${OBJS}
		${AOUT_RANLIB} $@

${OBJS}:	FRC

FRC:

$(SYSOBJS):	$(LIBCDIR)/$(MACHINE_ARCH)/sys/SYS.h
#		@echo creating $*.o
		@printf '#include "SYS.h"\nSYS($*)\n' | $(AS) $(ASFLAGS) - -c -o $*.o

# Build objects here instead of ${LIBCDIR} with BSD make.
.OBJDIR:	${.CURDIR}

install:	../libc.a
		${INSTALL} -d ${DESTDIR}/usr/lib
		${INSTALL} ../libc.a ${DESTDIR}/usr/lib/libc.a
		${AOUT_RANLIB} -t ${DESTDIR}/usr/lib/libc.a

clean:
		rm -f *~ *.o a.out *.a ../libc.a
