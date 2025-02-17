##
## EPITECH PROJECT, 2020
## Base
## File description:
## Main Makefile
##

##################### SRC #######################
SRC				=	src/create_struct/create_process.c					\
					src/create_struct/create_vm.c						\
					src/create_struct/create_champion.c					\
					src/create_struct/create_parsing.c					\
					src/create_struct/create_params.c					\
					src/destroy_struct/destroy_champion.c				\
					src/destroy_struct/destroy_vm.c						\
					src/destroy_struct/destroy_parsing.c				\
					src/destroy_struct/destroy_all.c					\
					src/parsing/get_info_champion.c						\
					src/parsing/get_flag.c								\
					src/init_struct/init_all.c							\
					src/init_struct/set_all.c							\
					src/init_struct/verif_file.c						\
					src/init_struct/verif_all.c							\
					src/init_struct/operation.c							\
					src/loop/main_loop.c								\
					src/loop/move_process.c								\
					src/loop/check_process.c							\
					src/loop/update_it.c								\
					src/loop/print_memory.c								\
					src/exec_instruct/exec_instruc.c					\
					src/exec_instruct/instruct/i_live.c					\
					src/exec_instruct/instruct/i_ld.c					\
					src/exec_instruct/instruct/i_st.c					\
					src/exec_instruct/instruct/i_add.c					\
					src/exec_instruct/instruct/i_sub.c					\
					src/exec_instruct/instruct/i_and.c					\
					src/exec_instruct/instruct/i_or.c					\
					src/exec_instruct/instruct/i_xor.c					\
					src/exec_instruct/instruct/i_zjmp.c					\
					src/exec_instruct/instruct/i_ldi.c					\
					src/exec_instruct/instruct/i_sti.c					\
					src/exec_instruct/instruct/i_fork.c					\
					src/exec_instruct/instruct/i_lld.c					\
					src/exec_instruct/instruct/i_lldi.c					\
					src/exec_instruct/instruct/i_lfork.c				\
					src/exec_instruct/instruct/i_aff.c					\
					src/exec_instruct/get_params.c						\
					src/exec_instruct/verif_params.c					\
					src/exec_instruct/write_params.c					\

SRC				+=	main.c

SRC				+=	../op.c

SRC_TEST		=


#################### NAMES ######################
NAME			=	corewar

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
