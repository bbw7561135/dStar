include $(MESA_DIR)/utils/makefile_header

DSTAR_LIB_DIR = ../../../lib
LOAD_LOCAL = -L$(LOCAL_LIB_DIR) -lmrcurve
LOAD_OTHER = -L$(DSTAR_LIB_DIR) -ldstar_crust -lconductivity -lneutrino -ldstar_eos -lsuperfluid -ldstar_atm -lnucchem -lconstants -L$(MESA_LIB_DIR) $(LOAD_MESA_NUMERICS)
DSTAR_INC = ../../../include

TEST = tester
TEST_OBJS = test_tov.o

default: install

$(TEST) : $(TEST_OBJS)
	$(LOADER) $(FCopenmp) -o $@ $(TEST_OBJS) $(LOAD_LOCAL) $(LOAD_OTHER)

compareEOS: compare_EOS.o
	$(LOADER) $(FCopenmp) -o $@ compare_EOS.o $(LOAD_LOCAL) $(LOAD_OTHER)

%.o: $(TEST_SRC_DIR)/%.f
	$(TEST_COMPILE) $(FCfree) $(FCimpno) -I$(DSTAR_INC) $<

install: $(TEST)
	cp $(TEST) ..
	mkdir -p ../LOGS

clean:
	-@rm -f *.o *.mod $(TEST) compareEOS
