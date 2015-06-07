targets = poll poll.man
bindir = ../`arch`
mandir = ../man

all:	$(targets)

# Should convert this to a doxygen extraction of comments in source file when I figure out how
%.man:  %.md
	pandoc -t man --standalone \
	    -V title="`echo $* | tr '[a-z]' '[A-Z]'`" \
	    -V section=1 \
	    -V date="`date '+%B %Y'`" \
	    -V description="\"Tarim\" \"User Commands\"" \
	    $< | \
	sed 's/\\\[em\]/--/g; s/---/\\-/g; 1a .nh\n.ad l' > $@.tmp
	if [ -s $@.tmp ]; then \
	    mv $@.tmp $@; \
	else \
	    rm $@.tmp; \
	fi

clean:
	rm -rf $(targets) *.tmp

install: force
	[ -d $(bindir) ] || mkdir $(bindir)
	cp -a poll $(bindir)
	cp -a poll.man $(mandir)

force:	clean
	make all
