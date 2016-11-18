.PHONY: all touch clean \
	    all@010-baseline \
	    all@020-incr-from-scratch \
	    all@030-incr-change-private-fn

all@010-baseline:
	cargo rustc $(CARGO_OPTS) -- $(CARGO_RUSTC_OPTS)

all@020-incr-from-scratch:
	find . -name "*.rs" | xargs touch
	RUSTFLAGS="-Z incremental=incr" cargo rustc $(CARGO_OPTS) -- \
	  $(CARGO_RUSTC_OPTS) -Z incremental-info

all@030-incr-no-change:
	find . -name "*.rs" | xargs touch
	RUSTFLAGS="-Z incremental=incr" cargo rustc $(CARGO_OPTS) -- \
	  $(CARGO_RUSTC_OPTS) -Z incremental-info

# all@030-incr-change-private-fn:
# 	find . -name "*.rs" | xargs touch
# 	RUSTFLAGS="-Z incremental=incr" cargo rustc $(CARGO_OPTS) -- \
# 	  $(CARGO_RUSTC_OPTS) -Z incremental-info

patches:
	@echo "@010-baseline \
	       @020-incr-from-scratch \
	       @030-incr-change-private-fn"

touch:
	find . -name "*.rs" | xargs touch

clean:
	rm -rf incr
