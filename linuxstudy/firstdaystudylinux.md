## The firstday study Linux
#### linux introduction
 Linuxϵͳ������1991��,������ѧ��ѧ������˹(Linus Torvalds)�ͺ���������ڶమ���߹�ͬ�������.Linux��һ���������,��Դ���뿪�ŵ�Unix.
###### ��������:
* ��ʱ�Ķ��û�,���������ϵͳ
* ��������Э��֧��,�����Զ�̹���
* ǿ����ڴ������ļ�ϵͳ����
* �����Ŀ��õ��������ѵ����
* �������ȶ��ԺͰ�ȫ��
* ���õĿ���ֲ�Ժ������
* �ɹ�ѡ��ĳ��̶�

###### Linux�����ķ��а汾
* RedHat Linux
* Fedora
* CentOS
* SuSE Linux
* Ubuntu Linux
* Mandrake Linux
* Caldera Linux
* Turbolinux
* Debian GNU/Linux
* Gentoo Linux
* Linpus Linux

###### Linux����ϵͳ�ṹ
![ͼƬ1.png](https://upload-images.jianshu.io/upload_images/14466054-1a742fe2a95d84e2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###### Windows���⻯��������
![ͼƬ2.png](https://upload-images.jianshu.io/upload_images/14466054-8a9e91b9b0eaa45a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
������������Ľ������:
* ����ȷ���Լ��ĵ�������������֧�����⻯����������ʵ�ָ����Լ��ʼǱ����ͺ�����
* ��סF2������Bios���ý��棬���ȿ�������main����Ҫ��ѡ�
* ѡ�����Advanced�߼���CPU Configuration  ����������
* �ҵ�Intel Virtualization TechnologyӢ�ض����⻯����ѡ��
* ����ΪEnabled��������F10�����˳�����

#### linuxĿ¼�ṹ
![QQͼƬ20181017195151.png](https://upload-images.jianshu.io/upload_images/14466054-e2cafdfdb623ebc7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###### Linuxϵͳ��������ػ�
* reboot
* shutdown -r now ��������(root�û�ʹ��)
* shutdown -r 10 ��10�����Զ�����(root�û�ʹ��)
* shutdown -r 20:35 ��ʱ��Ϊ20:35ʱ������(root�û�ʹ��)
* �����ͨ��shutdown�������������Ļ���������shutdown -c����ȡ������

* halt 	���̹ػ�
* poweroff 	���̹ػ�
* shutdown -h now 	���̹ػ�(root�û�ʹ��)
* shutdown -h 10 	10���Ӻ��Զ��ػ�

#### ��������

###### �޸�������
��ʱ�޸�
```
[root@localhost ~]# hostname
localhost.localdomain
[root@localhost ~]# hostname lanou 
[root@localhost ~]# hostname 
[root@lanou ~]#
```
�����޸�
* /etc/hostname�ļ�
* ��;:����ȫ���������ã���Ҫ������������Ϣ
* lanou     //�趨������

###### ping����
* ����������ͨ��
* ��ʽ:ping [ѡ��] Ŀ������
```
[root@localhost ~]# ping 192.168.4.110
PING 192.168.4.110 (192.168.4.110) 56(84) bytes of data.
64 bytes from 192.168.4.110: icmp_seq=1 ttl=128 time=0.694 ms
64 bytes from 192.168.4.110: icmp_seq=2 ttl=128 time=0.274 ms
����
```

###### �鿴����ӿ���Ϣ
* �鿴���л����ӿڵ���Ϣ
* ִ�� ifconfig����
* �鿴ָ������ӿ���Ϣ
* ��ʽ:ifconfig	����ӿ���
* Ifconfig������,ʹ��yum���� 
* yum install net-tools

###### �������������ͼ
![ͼƬ3.png](https://upload-images.jianshu.io/upload_images/14466054-7704e7ae850813cf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###### ���÷���ǽ
* �鿴����ǽ״̬
* service firewalld status
* centos7�رշ���ǽ
* //��ʱ�ر�
* systemctl stop firewalld
* //��ֹ��������
* systemctl disable firewalld

###### ��������ӳ���ļ�
* /etc/hosts �ļ�
* ��;:������������IP��ַ��ӳ���¼
```
[root@localhost ~]# cat /etc/hosts
127.0.0.1		localhost.localdomain  localhost
......
119.75.218.70	 www.baidu.com
```
![ͼƬ4.png](https://upload-images.jianshu.io/upload_images/14466054-450135847156f37f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###### ����SELinux
* �鿴SElinux,���ܷ��صĽ��������
* Enforcing:ǿ��ģʽ�������¼��ȫ��������ֹ������Ϊ
* Permissive:����ģʽ�������¼��ȫ���浫����ֹ������Ϊ
* Disable:�ر�
* ��ǰ��Ч
setenforce	[ Enforcing \ Permissive\ 1\ 0 ]
��������������ı�SELinux����״̬����Enforcing ��Permissive  ֮���л����ػ�����֮��ʧЧ.
* ������Ч
�޸������ļ�/etc/selinux/config,��SELINUX=enforcing�޸�ΪSELINUX=disabled������Ч

#### ��ϤLinux��������
###### Linux����Ļ�����ʽ
* Linux�����ͨ�������ʽ
* ������  [ѡ��]  [����]
* ѡ������ĺ���
* ѡ����ڵ�������ľ��幦��
* ��������������Ķ���,���ļ�Ŀ¼����

* ls����ʾ�ļ���Ŀ¼�б�(list)
* ���ò���:
* -l (long)
* -a(all)         ע�������ļ�������Ŀ¼.��..   
* -t	(time)

###### Linux���������
* �ڲ��������Shell��������һ����
cd �л�Ŀ¼(change directory)
pwd ��ʾ��ǰ����Ŀ¼(print working directory)
help ����
* �ⲿ����:������Shell������֮����ļ�����
ls ��ʾ�ļ���Ŀ¼�б�(list)
mkdir ����Ŀ¼(make directoriy)
cp �����ļ���Ŀ¼(copy)
* �鿴�����ĵ�
�ڲ�����:help + ����(help cd)
�ⲿ����:man + ����(man ls)

###### ʹ����������ļ���Ŀ¼
* Ŀ¼��������
pwd cd ls mkdir du
* �ļ���������
touch file cp rm mv which find
* �ļ����ݲ�������
cat more less head tail wc grep
* ѹ������
gzip bzip2 tar

###### Ŀ¼��������
* pwd����
��;:�鿴����Ŀ¼(Print Working Directory)
* cd����
��;���л�����Ŀ¼(Change Directory)
��ʽ��cd   [Ŀ¼λ��]
* ls����
��;:�б�(List)��ʾĿ¼����
��ʽ:ls	[ѡ��]...  [Ŀ¼���ļ���]
��������ѡ��
-l :��ϸ��Ϣ��ʾ
-a:��ʾ������Ŀ¼���ļ�����Ϣ�����������ļ�
-A:�����ڡ�-a��,������ʾ��.���͡�..��Ŀ¼����Ϣ
-R:�ݹ���ʾ����

####### �ļ���������
* touch����
��;:�½����ļ���������ļ�ʱ����
��ʽ:touch	�ļ���
* file����
��;:�鿴�ļ�����
��ʽ: file   �ļ���
* cp����
��;:����(copy)�ļ���Ŀ¼
��ʽ:cp   [ѡ��]    Դ�ļ���Ŀ¼��   Ŀ���ļ���Ŀ¼
��������ѡ��
-r:�ݹ鸴������Ŀ¼��
-p:����Դ�ļ������Բ���
-f:ǿ�Ƹ���Ŀ��ͬ���ļ���Ŀ¼
-i:��Ҫ�����ļ���Ŀ¼ʱ��������
* rm����
��;:ɾ��(Remove)�ļ���Ŀ¼
��ʽ:rm   [ѡ��]   �ļ���Ŀ¼
��������ѡ��
-f:ǿ��ɾ���ļ�������������
-i:ɾ���ļ�ʱ�����û�ȷ��
-r:�ݹ�ɾ������Ŀ¼��
* mv����
��;:�ƶ�(Move)�ļ���Ŀ¼���� ���Ŀ��λ����Դλ����ͬ,���൱�ڸ���
��ʽ:mv   [ѡ��]...   Դ�ļ���Ŀ¼...  Ŀ���ļ���Ŀ¼























