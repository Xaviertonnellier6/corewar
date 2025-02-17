##
## EPITECH PROJECT, 2020
## Base
## File description:
## Main Makefile
##

##################### SRC #######################
SRC				=	src/check_asm.c					\
					src/check_command.c				\
					src/check_header.c				\
					src/check_params_size.c			\
					src/check_synthaxe.c 			\
					src/destroy_command.c			\
					src/get_command_name.c			\
					src/get_command_params.c		\
					src/get_command.c				\
					src/swap_endian.c				\
					src/write_asm.c					\
					src/write_info.c				\
					src/write_instructon.c			\
					src/write_label.c				\
					src/write_name.c				\
					src/get_size.c					\
					src/is_type.c					\

SRC				+=	main.c

SRC				+=	../op.c

SRC_TEST		=


#################### NAMES ######################
NAME			=	asm

NAME_TEST		=	unit_tests


##################### OBJ #######################
OBJ				=	$(SRC:.c=.o)

OBJ_TEST		=	$(SRC_TEST:.c=.o)


##################### FLAGS #####################
CFLAGS			=	-I include -I ../include -L ../lib/ -lblib -llinked_list -Wall -Wextra -W

CFLAGS_TEST		=	--coverage -lcriterion

CFLAGS_DEBUG	=	-g


################## COMPILATION ##################
$(NAME):	$(OBJ)
	@make -C ../lib/blib
	@make -C ../lib/linked_list
	@(gcc $(OBJ) -o $(NAME) $(CFLAGS)) > /dev/null

all:	$(NAME)

debug:	CFLAGS += $(CFLAGS_DEBUG)
debug:	re

re:	fclean all

clean:
	@(make clean -C ../lib/blib) > /dev/null
	@(make clean -C ../lib/linked_list) > /dev/null
	@(rm -f $(OBJ)) > /dev/null
	@find . -name "*.gcno" -delete
	@find . -name "*.gcda" -delete
	@find . -name "*.o" -delete

fclean:	clean
	@(make fclean -C ../lib/blib) > /dev/null
	@(make fclean -C ../lib/linked_list) > /dev/null
	@rm -f $(NAME)
	@(rm -f $(NAME) $(NAME_TEST)) > /dev/null
	@(rm -rf tests/coverage) > /dev/null
	@$(ECHO) $(CLEAR)

unit_tests:	$(OBJ_TEST)
	gcc -o $(NAME_TEST) $(OBJ_TEST) $(SRC) $(CFLAGS_TEST) $(CFLAGS)
	./$(NAME_TEST)

tests_run:	clean unit_tests

gcovr:	tests_run
	@gcovr --exclude tests
	@gcovr --exclude tests --branch

gen_html:	unit_tests
	@(mkdir -p tests/coverage) > /dev/null
	@(lcov -c -d . --output-file tests/coverage/lcov) > /dev/null
	@(genhtml tests/coverage/lcov --output-directory tests/coverage) > /dev/null

html_run:	gen_html
	@(firefox tests/coverage/index.html) > /dev/null
