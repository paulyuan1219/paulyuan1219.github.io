# Linux

    sort -t , -k14,14 -k15,15 -k8,8 540.nohead.csv > 540.nohead.sort.csv
    cut -d, -f 14,15 540.nohead.sort.csv > a
    sed 's/,/       /g' 70.nohead.sortbycol89.col789.csv > 70.nohead.sortbycol89.col789.tab.csv    
    sed -n 1,22p d > d00 # extract l1 to l22
    
