nova network-create vmnet --fixed-range-v4=192.168.3.0/24 --bridge=br100 --multi-host=T

nova boot --flavor m1.tiny --key_name mykey --image fbcbc4bd-6cd2-4dd7-986a-6d660c2551a7 CirrOS_Test

nova boot --flavor 1 --key_name mykey --image fbcbc4bd-6cd2-4dd7-986a-6d660c2551a7 --security_group default cirrOS

