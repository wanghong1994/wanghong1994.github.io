# The Third Day Study Hadoop
### hadoop��ȫ�ֲ�ʽ�Ĵ���
#### һ��.xshell�ϵķ��ͼ���������лỰ�Ĺ��ܵ�ʹ��
- ���������µ������,ȫ����xsheel��,�����������Ҫ����hadoop�û�,�������Ŀ¼��,����jdk��hadoopѹ����.
- �Ҽ�,ѡ���ͼ���������лỰ,������һ��������н�ѹjdkhadop.����������������Զ�ͬ��.
- ���ú�jdk��hadoop����

##### ʹ��scp�����֮ǰ��õ�α�ֲ�ʽ��5��.xml�ļ������ݴ��͵����ڵ������½��������.

```
��ʽ:scp Ҫ��������� Ҫ�����ĵ��Ե��û���@Ҫ�����ĵ��Ե�IP:Ҫ��������̨���Ե�λ��
����:
scp -r /home/tars/hadoop-2.7.3/etc/hadoop hadoop@172.18.24.190:/home/tars/hadoop-2.7.3/etc/hadoop
Ҫ����������֮ǰα�ֲ�ʽ���úõ�hadoop��ѹ���µ�etc�ļ����µ�hadoop�ļ���
Ҫ��������hadoop�û�,ip��172.18.24.190.
Ҫע��Ȩ��,���Ȩ�޶���root,ʹ��chown -R hadoop:hadoop /home/tars/hadoop-2.7.3/etc/hadoop���������hadoop�ļ�Ȩ��ȫ���ĳ�hadoop�û�,����ʹ��suȨ��
�ظ�����,ע��ip��ַ,��ʣ����̨�������hadoop���ļ��滻��.
```

###### ע��:�½�������������ǵ���datanodeʹ�õ�,֮ǰ������α�ֲ�ʽ����namedata,���ϲ�����ʵ��Ҫ��jdk��hadoop��������,�Լ���namenodeͬ��������datanode��.����Ͳ���Ҫ���и�ʽ����,��ʽ�������namenode���е�
#### ��.��hadoop��ѹ����etc�µ�hadoop�ļ����µ�slaves�ļ�������½��������������IP��ַ(��Ϊ��datanodeд��ȥ����ע��)
#### ��.���ܲ���(������namenode�ϲ���)
- ע��������:ssh-keygen(��ȡע����,����д����ĵط�ֱ�ӻس�,��Ϊ���������ر�ʱ����Ҫ����)
- ִ������:ssh-copy-id hadoop@172.18.24.190 (���ִ������,ÿ�ε�IP��ַд�½�������������ĵ�ַ)
- ִ����:cat id_dsa.pub >> ~/.ssh/authorized_keys(��.pub�ļ����Ƶ� .ssh Ŀ¼��)
- �鿴���������datanode������:hdfs dfsadmin -report

#### ��.����ҳ�ϵ�¼namenode,����datanodeû���������뵽namenode�ϵĽ������
- �ҵ�datanode�������hadoop�Ľ�ѹ���µ�logs�ļ����µ�namenode��log�ļ���,�ᷢ��hostname�Ĵ���.��ʱ,��namenode��/etc/hosts�ļ����������datanode��namenode�������ip�Ͷ�Ӧ����ȡ�����ּ���.
	- ����: 172.18.24.251  datanode1
	- 172.18.24.20 namenode