# Pendahuluan - KVM

KVM adalah salah satu perangkat lunak opensorce yang di gunakan untuk memanage virtual machine. Tidak seperti perangkat lunak lain yang sejenis, kvm lebih mengedepankan menggunakan CLI untuk pengoprasional nya, sehingga kvm sangat powerfull apabila digunakan menggunakan automasi, dan atau alat pendukung cloud computing seperti Openstack. Berikut merupakan contoh architecture KVM yang develop oleh redhat.

<figure><img src="../../.gitbook/assets/image (27).png" alt=""><figcaption><p><strong>RHEL 8 virtualization architecture</strong></p></figcaption></figure>

Seperti yang kita bahas sebelum nya KVM sangat powerfull apabila pengoprasionalan nya menggunakan automasi, beberapa pihak ketiga yang dapat digunakan untuk memanage kvm adalah terraform, ansible, dan untuk web based nya bisa menggunakan cockpit.&#x20;

Untuk selebih nya dapat di baca pada website&#x20;

{% embed url="https://www.linux-kvm.org/page/Management_Tools" %}

{% embed url="https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/configuring_and_managing_virtualization/introducing-virtualization-in-rhel_configuring-and-managing-virtualization#what-is-virtualization_introducing-virtualization-in-rhel" %}
