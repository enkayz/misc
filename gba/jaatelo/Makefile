# Makefile for valot.
#
# Programs used to compile: 
# arm-elf-gcc 3.4.1 
# gba-header Mac OS X (http://velvetfr.ath.cx/)
#
# Copyright (C) 2004 Sakari Lehtonen <sakari@ionstream.fi>
#

# Programs
CROSS = arm-eabi-
CC = $(CROSS)gcc
AS = $(CROSS)as
STRIP = $(CROSS)strip
OBJCOPY = $(CROSS)objcopy
GBA_HEADER = gbafix

# My GBA lib stuff
LGLDIR = ../lgl
INCLUDES = -I$(LGLDIR) 
LIBPATHS = -L$(LGLDIR)
# Not really using the lgl library, just these objects from it
LGL_OBJS = $(LGLDIR)/memory.o $(LGLDIR)/bg.o $(LGLDIR)/fonts_bg.o \
	   $(LGLDIR)/sprites.o $(LGLDIR)/input.o


# Flags
COMFLAGS = -mthumb-interwork
CFLAGS = $(INCLUDES) $(COMFLAGS) -Wall -O2
LDFLAGS = -specs=gba.specs $(COMFLAGS) $(LIBPATHS) $(LIBS)

# Project specific 
PROJECT = jaatelo
OBJECTS = $(PROJECT).o posprintf.o $(LGL_OBJS)
DATAOBJS = data_font.o data_player.o data_car.o data_missile.o \
	   data_explosion.o

# Compilation rules
$(PROJECT).gba: $(PROJECT).elf
	$(OBJCOPY) -O binary $(PROJECT).elf $@
	$(GBA_HEADER) $@ -title $(PROJECT)

$(PROJECT).elf: $(OBJECTS) $(DATAOBJS)
	$(CC) $(LDFLAGS) $(OBJECTS) $(DATAOBJS) -o $@

.c.o: 
	$(CC) $(CFLAGS) -c -o $@ $<
.S.o:
	$(AS) $(COMFLAGS) -o $@ $<

clean:
	rm -rf $(PROJECT).gba *.o *.elf
