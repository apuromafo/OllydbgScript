                                    **ʹ��ǰ���޸�**

��ѹ�����е� Asprvm8s.bin ����һ����ָ���ĵط�, Ȼ���ü��±��޸Ľű��е�����


lab78_1:
log VMcodeloc
lm VMcodeloc, 4000, "d:\Asprvm8s.bin"         ---> �޸����


�����ǰ� Asprvm8s.bin ���� c:\script ��Ŀ¼������������ĳ�


lm VMcodeloc, 4000, "C:\script\Asprvm8s.bin"


Ȼ��浵.



                            **Modification needed before usage**

Copy the Asprvm8s.bin into a folder you want , then use text editor to modify this part of the script


lab78_1:
log VMcodeloc
lm VMcodeloc, 4000, "d:\Asprvm8s.bin"         ---> modify this line


if Asprvm8s.bin is copied under the folder c:\script the above command should be chnaged as


lm VMcodeloc, 4000, "C:\script\Asprvm8s.bin"



