ifeq (,$(OUT))
$(error you must define OUT)
endif

TMP = .tmp

HTML_NAMES = $(addsuffix .html, index contact venue registration	\
 schedule/index speakers/index kickstarter/index)

TALK_BASENAMES = alexandrescu bright buclaw cehreli chevalier_boisvert	\
 clugston edwards evans_1 evans_2 gertzfield lucarella nadlinger		\
 nowak olshansky panteleev rohe schadek schuetze simcha wilson

TO_COPY = images/ includes/ $(addsuffix .pdf, $(addprefix talks/,	\
bright buclaw cehreli schadek gertzfield evans_1 lucarella nowak wilson \
panteleev schuetze chevalier_boisvert clugston rohe nadlinger evans_2 \
alexandrescu))

TALK_NAMES = $(addprefix talks/, $(addsuffix .html, ${TALK_BASENAMES} panel))

SPEAKER_BITS = $(addprefix $(TMP)/speakers/, $(addsuffix .gen.ddoc, ${TALK_BASENAMES}))

SCHEDULE_BITS = $(addprefix $(TMP)/schedule/, $(addsuffix .gen.ddoc, ${TALK_BASENAMES}))

ALL_RELATIVE_PATHS = $(HTML_NAMES) $(TALK_NAMES) $(TO_COPY)

SITE_FILES = $(addprefix $(OUT)/, $(ALL_RELATIVE_PATHS))

# Rules

all : $(SITE_FILES)

clean :
	rm -rf $(OUT) $(TMP)

# Patterns

$(OUT)/talks/%.html : macros.ddoc talks/macros.ddoc talks/%.dd
	dmd -c -o- -Df$@ $^

$(TMP)/speakers/%.gen.ddoc : macros.ddoc speakers/fragment.ddoc talks/%.dd
	dmd -c -o- -Df$@ $^

$(OUT)/speakers/index.html : macros.ddoc ${SPEAKER_BITS} speakers/index.dd
	dmd -c -o- -Df$@ $^

$(OUT)/schedule/index.html : macros.ddoc ${SCHEDULE_BITS} $(TMP)/schedule/panel.gen.ddoc \
		schedule/index.dd
	dmd -c -o- -Df$@ $^

$(TMP)/schedule/%.gen.ddoc : macros.ddoc talks/macros.ddoc schedule/fragment.ddoc talks/%.dd
	dmd -c -o- -Df$@ $^

$(OUT)/kickstarter/%.html : macros.ddoc kickstarter/%.dd
	dmd -c -o- -Df$@ $^

$(OUT)/%.html : macros.ddoc %.dd
	dmd -c -o- -Df$@ $^

$(OUT)/%/ : %/
	cp -r $^ $@

$(OUT)/%.pdf : %.pdf
	cp $^ $@

