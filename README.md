# eslpred2
# put every seq. in separated file
cat *.fasta |\
awk '/^>/ {if(N>0) printf("\n"); printf("%s\n",$0);++N;next;} { printf("%s",$0);} END {printf("\n");}' |\
split -l 2 --additional-suffix=.fa - seq_
# renaming the files
for i in *.fa; do mv $i $(head -1 $i | cut -f1 -d ' ' | tr -d '>' ).fa; done
# running the eslpred2
for file in *.fa; do ./eslpred2.pl -i $file -o $file.out
