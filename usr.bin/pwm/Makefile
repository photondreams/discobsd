#
# Public Domain.  1995/03/13 - Steven Schultz
#
TOPSRC!=cd ../..; pwd
include ${TOPSRC}/share/mk/sys.mk

CFLAGS		+= -Wall

SRCS            = pwm.c
OBJS            = pwm.o

all:            pwm

pwm:    ${OBJS}
		${CC} ${CFLAGS} ${LDFLAGS} -o pwm.elf ${OBJS} ${LIBS}
		${OBJDUMP} -S pwm.elf > pwm.dis
		${SIZE} pwm.elf
		${ELF2AOUT} pwm.elf $@

.SUFFIXES:      .0 .1

clean:
		rm -f *.o *.elf *.elf *.dis tags *~ pwm

depend:         ${SRCS}
		mkdep ${CFLAGS} ${SRCS}

install:        all
		${INSTALL} -m 755 pwm ${DESTDIR}/usr/bin

lint:           ${SRCS}
		lint -hax ${SRCS}

tags:           ${SRCS}
		ctags ${SRCS}
