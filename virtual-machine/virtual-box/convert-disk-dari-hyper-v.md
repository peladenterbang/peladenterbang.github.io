# Convert disk dari hyper-v

Convert disk ini bertujuan saat ingin menggunakan disk yang sama dari hyper-v ke virtual box.



Buka \`power shell\` menggunakan administrator permission. lalu eksekusi perintah berikut

```
Convert-VHD -Path d:\VM\JANGAN-DIDELETE\ubuntu.vhdx -DestinationPath d:\VM\JANGAN-DIDELETE\converted-ubuntu.vhd
```

source path : file disk hyper-v&#x20;

destination : hasil convert disk&#x20;

anda bisa menggunakan disk converted-ubuntu.vhd pada virtualbox menggunakan disk dari vm hyper-v sebelum nya.
