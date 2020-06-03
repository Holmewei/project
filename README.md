LOPATH=/data/UPitouzi/xf_ccs
SVNPATH=

mkdir -pv $LOPATH/PC_ecshop
cd $LOPATH

echo "svn代码更新"
/usr/bin/svn co svn://192.168.23.238/website2v/trunk/ccs_xf > uplist.file
/usr/bin/svn co svn://192.168.23.238/website2v/trunk/thirdlib > uplist.file
/usr/bin/svn co svn://192.168.23.238/website2v/trunk/itzlib > uplist.file
#/usr/bin/svn co svn://172.17.139.87/ecshop/branches/feilinghe_ecshop PC_ecshop/shop >> uplist.file
echo "本地拷贝开始"
rsync -avz $LOPATH/  --exclude=PC_ecshop --exclude=.svn  --delete  $LOPATH/PC_ecshop  2>>$LOPATH/s.log 1>/dev/null
echo "本地拷贝完成"
cd $LOPATH/PC_ecshop
chown -R nginx:nginx *
rsync -avz ./*  static@47.93.242.232::wx_dashboard --password-file=/etc/rsync/clinet/xf_ccs.db


