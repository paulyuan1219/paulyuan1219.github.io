# Linux

    sort -t , -k14,14 -k15,15 -k8,8 540.nohead.csv > 540.nohead.sort.csv
    cut -d, -f 14,15 540.nohead.sort.csv > a
    
