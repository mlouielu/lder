CC = gcc
OBJCOPY = objcopy
CFLAGS = -m32


OBJS = simple_section.o
LENA = l_hires

%.o: %.c
	$(CC) $< -c $(CFLAGS) -o $@


all:	$(OBJS)

lena:
	$(OBJCOPY) -I binary -O elf32-i386 -B i386 $(LENA).jpg $(LENA).o

clean:
	$(RM) $(OBJS) $(LENA).o

