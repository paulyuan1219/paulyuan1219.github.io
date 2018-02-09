# Linux

    sort -t , -k14,14 -k15,15 -k8,8 540.nohead.csv > 540.nohead.sort.csv
    cut -d, -f 14,15 540.nohead.sort.csv > a
    sed 's/,/       /g' 70.nohead.sortbycol89.col789.csv > 70.nohead.sortbycol89.col789.tab.csv    
    sed -n 1,22p d > d00 # extract l1 to l22
    egrep '^-1,' query_tbcat.csv.new.output_1.tmpnew.autoeval > a2
    iconv -c -f GB2312 -t utf-8 infile > outfile
    tar -xvzf *.tar.gz
    conda create --name py36 python=3.6 numpy scipy matplotlib pandas anaconda
    conda create --name py27 python=2.7 numpy scipy matplotlib pandas anaconda
    iconv -c -f GB2312 -t UTF-8 test_query.csv > test_query.csv.new
    
