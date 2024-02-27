# Ferramentas do toolchain

Compila = arm-none-eabi-gcc
Remove = rm -rf

# Diretório onde os arquivos objetos serão salvos

diretoriobj = build
diretoriodep = .deps

# Arquivos a serem compilados

arqcomp = startup.c \
        main.c

#Flags do compilador e linker

CFLAGS = -g -mcpu=cortex-m4 -mthumb -Wall -O0
DEPFLAGS = -MMD -MP -MF $(diretoriodep)/$*.d

# Gera uma lista de arquivos objeto utilizando os arquivos fonte

objetos = $(patsubst %, $(diretoriobj)/%.o, $(basename $(arqcomp)))
$(shell mkdir -p $(dir $(objetos)) > /dev/null)

# Gera lista de arquivos de dependencia e cria o diretório onde serão armazenados

deps = $(patsubst %, $(diretoriodep)/ %.d, $(basename $(arqcomp)))
$(shell mkdir -p $(dir $(deps)) > /dev/null)

all: $(objetos)

$(diretoriobj)/%.o: %.c $(deps)/%.d
	$(Compila) -c $(CFLAGS) $(DEPFLAGS) $< -o $@

.PHONY: clean
clean:
	$(Remove) $(diretoriobj) $(diretoriodep)