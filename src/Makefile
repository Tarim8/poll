targets = poll poll.man
bindir = ../`arch`
mandir = ../man

all:	$(targets)

# Should convert this to a doxygen extraction of comments in poll.cc when I figure out how
poll.man:  poll.md
	pandoc -t man $< | \
	sed 's/\\\[em\]/--/g; s/---/\\-/g; 1s/\\\[[rl]q\]/"/g; 1s/^\.S[SH]/.TH/; 1a .nh\n.ad l' > $@.tmp
	if [ -s $@.tmp ]; then \
	    mv $@.tmp $@; \
	else \
	    rm $@.tmp; \
	fi

clean:
	rm -rf $(targets) *.tmp

install: all
	[ -d $(bindir) ] || mkdir $(bindir)
	cp -a poll $(bindir)
	cp -a poll.man $(mandir)

force:	clean
	make all
