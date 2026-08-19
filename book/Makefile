# 1. Dossier contenant les figures TikZ
TIKZ_DIR = tikz

# 2. Lister tous les fichiers .tex dans ce dossier
SRCS = $(wildcard $(TIKZ_DIR)/*.tex)

# 3. Déduire les fichiers .svg cibles attendus
SVGS = $(SRCS:.tex=.svg)

# Cible par défaut
all: $(SVGS)

# 4. Règle de production globale (Tex -> SVG)
$(TIKZ_DIR)/%.svg: $(TIKZ_DIR)/%.tex
	@echo "[Make] Traitement de $<..."
	
	@# Étape A : Compilation LaTeX classique dans le dossier tikz
	latex -interaction=batchmode -output-directory=$(TIKZ_DIR) $<
	
	@# Étape B : Conversion en SVG sans polices (vectorisation pure -n) et recadré
	dvisvgm --no-fonts $(TIKZ_DIR)/$*.dvi -o $(TIKZ_DIR)/$*.svg
	
	@# Étape C : Nettoyage immédiat du DVI et des journaux LaTeX
	rm -f $(TIKZ_DIR)/$*.dvi $(TIKZ_DIR)/$*.aux $(TIKZ_DIR)/$*.log

# Nettoyage complet
clean:
	@echo "[Make] Suppression des fichiers SVG générés..."
	rm -f $(SVGS)

.PHONY: all clean
