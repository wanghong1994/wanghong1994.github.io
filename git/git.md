# githubʹ��

pwd �鿴��ǰ�����ļ�·��
ls  �鿴�ļ������ļ�
mkdir �����ļ���
touch �����ļ�
git status �鿴�ļ���״̬
git add ����ļ�

ls  �鿴�ļ������ļ�

mkdir �����ļ���
touch �����ļ�

git status �鿴�ļ��е�ǰ�ļ��Ƿ������޸Ĺ���
git add ����ļ�·��




����github���Ƴ��ļ���

��һ��:

$ git clone

���Լ���github��Դ��,����ұ�clone and download ,��ssh,����·��ssh��ʽ
��ָ��git clone �������·��
ȷ����������yesȷ��

�ڶ���:���ù�Կ

$ ssh-keygen -t rsa -C "�����ַ"
���λس�

���ҵĵ��Դ��û�.....��.ssh�ļ���,�Լ��±���ʽ��id_rsa.pub

���Լ���github���û�����,���ssh and GPG keys ,��ӹ�Կ,��������,���±�id_rsa.pub
ȫ���Ƶ���Կ��
�ٴ�ִ��git clone����

git config --global user.email "�����ַ"(��һ��ƥ���µĵ�������Ҫ��Կ�������ʹ��)

git config --global user.name "�û���"(��һ��ƥ���µĵ�������Ҫ��Կ�������ʹ��)

git commit

git push -u origin master(�ֿ��ǲŴ���,��һ���ϴ��ļ�ʱ Ҫдȫ)

git push (�ڶ��μ��Ժ� ֱ������д)



git ����
	git add �ļ�·�� �ô����������ļ�����git�ֿ�Ҫ���

	git commit -m ��Ҫ�ύ��������ʲô---�ύ��־�� ���������Ĳ����ύ������git�ֿ�

	git push -u origin master ����һ����ôд��Ŀ���������Ժ�Ĭ�϶�����master��֧���ύ���룩

	git pull    ���±��زֿ⣬ʹ���غ�githubͳһ

	echo "����" >> Ҫ��ӵ����ļ�����

��������ͻ

	git stash   ��ջ�����أ�

	git pull

	git stash pop   ��ջ


git add 

ls -all չʾ�����ļ�

rm -rf .git/  ǿ��ɾ�� .git/ ������


git ���˺���

git init ��ʼ��git�ֿ�(.git�ļ�������)

git remote add origin git@github.com:�û���/project.git     ȷ�ϱ��غ�Զ�ֿ̲�����

�տ�ʼ��ʼ��������git�ֿ��ǲ�֪�����͵�Զ��git�ֿ���˭,

������Ҫ�����������Ҫ���Ķ���Զ�ֿ̲�����

1.github ����һ�����ڶ��˺�����git�ֿ�

2.���Ͱ汾�Ĵ���,���ݵ����ǵĲֿ���

3.Ĭ��������Ķ����˺Ŵ����Ĳֿ�,ֻ�б������ύ��������,�����Ҫ���˿���,��Ҫ������˳�ΪЭ����