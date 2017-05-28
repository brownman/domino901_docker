#install
1. docker build -t test/domino1 .

#wrap
2. docker build -t test/dominosetup .

#run
3.docker run -p -v notesdata:/local/notesdata test/dominosetup
