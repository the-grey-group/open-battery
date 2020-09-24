# open-battery

Steps for installing and running initial commands.

1. Follow instructions in the ami3 repo for installing ami3 and maven:

https://github.com/petermr/openVirus/blob/master/INSTALLING.md

2. Make sure ami is in PATH according to installation instructions:

```
This gives an executable in <your dir>/ami3/target/appassembler and you should set your PATH to include <your dir>/ami3/target/appassembler/bin
```

3. Test ami is working, and git pull and rebuild with maven if necessary for latest version (from inside the main ami3 directory).
```
ami --help

git pull

mvn clean install -Dmaven.test.skip=true 
```

4. Create subdirectory with downloaded PDF files, for example, called batterypapers, and the make a new project.
```
ami -p batterypapers makeproject --rawfiletypes pdf
```


5. Extract pdfs and set each in their own folder
```
ami -p batterypapers pdfbox
```

6. Produce a subdirectory in each pdf with separate images
```
ami -p batterypapers image
```
7. Produce images scaled up, and with sharpened text
```
ami -p batterypapers --inputname raw image --scalefactor 2.0
ami -p batterypapers --inputname raw image --sharpen sharpen8
```
8. Test to select lines within a figure corresponding to data
```
ami -p batterypapers --inputname raw pixel
```

9. One line command to do OCR with tesseract.
```
ami -p batterypapers --inputname raw ocr --html true --tesseract=/opt/local/bin/tesserlefactor 2.0
```
Manually pointing to where tesseract is installed, in this case:
```
/opt/local/bin/
```

10. Complete one line command:
```
ami -p <targetDir> --inputname raw -v pdfbox filter -sdm image --posterize 4 ocr --html true --tesseract=/opt/local/bin/tesserlefactor 2.0
```

11. Using ami section to extract table and figure information:
```
ami -p liion -v --forcemake section --extract tab fig --summary fig tab
```
