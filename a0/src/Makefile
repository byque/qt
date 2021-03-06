################################################################################
# Plantilla de Makefile con funciones avanzadas                                #
################################################################################

# Éste es el nombre de los binarios que serán generados
TARGET   = holabinario

# Algunas rutas (por defecto debería funcionar)
QTLIBS_ROOT = /usr/share/qt4/include
QTLIBS      = $(QTLIBS_ROOT)/QtGui

# Aquí añadimos todos los archivos *.cpp que se quieren compilar
CPPSRCS  = holafuncion.cpp holamain.cpp

# Aquí añadimos las rutas a los directorios include
IDIR     = ../include

# Aquí añadimos las librerías estándar que se van a usar
LIBS     = -lQtGui -lQtCore

# Configuración del compilador
CPPC     = g++
CPPFLAGS = -g -std=c++11 -Wall
LDFLAGS  = -g -Wall

################################################################################
# No cambiar nada después de esta línea                                        #
################################################################################

BINDIR   = ../bin
BUILDDIR = ../build
OBJDIR   = $(BUILDDIR)/obj

# Generar el nombre de los archivos objeto
OBJS = $(addprefix $(OBJDIR)/,$(addsuffix .o,$(basename $(CPPSRCS:%.c=%.o))))

# Añadir las rutas
CPPFLAGS += $(IDIR:%=-I %) -I $(QTLIBS_ROOT) $(QTLIBS:%=-I %)
LDFLAGS  += $(IDIR:%=-I %)

# Añadir las librerías estándar
LDFLAGS   += $(LIBS)

# Aquí se definen los archivos generados por defecto cuando el usuario llama
# solamente 'make'
all: build size

# Crear todos los archivos y el binario
build: builddirs $(BINDIR)/$(TARGET)

# Crear los directorios requeridos (si no existen previamente)
builddirs:
	@echo
	@echo "Creando directorios..."
	@mkdir -p $(BINDIR)
	@mkdir -p $(BUILDDIR)
	@mkdir -p $(OBJDIR)

# Enlazar todo junto
$(BINDIR)/$(TARGET): $(OBJS)
	@echo
	@echo Enlazando $@
	@$(CPPC) $(LDFLAGS) -o $(BINDIR)/$(TARGET) $(OBJS)

# Compilar los archivos en c++
$(OBJDIR)/%.o: %.cpp
	@mkdir -p $(dir $@)
	@echo
	@echo Compilando $^
	@$(CPPC) $(CPPFLAGS) -c -o $@ $^

# Imprimir la información del tamaño
size: $(BINDIR)/$(TARGET)
	@echo
	size $^

# Limpiar código
clean:
	@echo
	@echo "Limpiando..."
	@rm -rf $(BINDIR) $(BUILDDIR) $(OBJS) $(TARGET) $(TARGET).* *.a *.o *~
	@echo
	@echo "Limpieza terminada!"

# Clean debe ser phony tal que make nunca salga de ejecución como un archivo
.PHONY: clean
