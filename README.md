# CFSSL

|Go.x509.KeyUsage|CFSSL config.json| id-ce-keyUsage|Comment|
|-----|-----|-----|-----|
|KeyUsageDigitalSignatureKeyUsage|digital signature|digitalSignature||
|KeyUsageContentCommitment|content commitment|nonRepudiation|recent editions of X.509 have renamed this bit to contentCommitment|
|KeyUsageKeyEncipherment|key encipherment|keyEncipherment||
|KeyUsageDataEncipherment|key agreement|dataEncipherment||
|KeyUsageKeyAgreement|data encipherment|keyAgreement||
|KeyUsageCertSign|cert sign|keyCertSign||
|KeyUsageCRLSign|crl sign|cRLSign||
|KeyUsageEncipherOnly|encipher only|encipherOnly||
|KeyUsageDecipherOnly|decipher only|decipherOnly||


````
docker run -ti -v c:\docker/srv:/shared cfssl /bin/sh
cfssl gencert -initca ca_csr.json  | cfssljson -bare /shared/hasCA

cfssl gencert -ca /srv/hasCA.pem -ca-key /shared/hasCA-key.pem -config="config.json" -profile="intermediate" ica-csr.json | cfssljson -bare /shared/hasICA

cfssl gencert -ca /srv/hasICA.pem -ca-key /shared/hasICA-key.pem -config=config.json -profile="server" destek.csr.json |cfssljson -bare /shared/destek

cat /srv/hasICA.pem /srv/hasCA.pem > /srv/hasCA-chain.pem



openssl verify -CAfile /srv/hasCA.pem /srv/hasICA.pem

cat /srv/hasICA.pem /srv/hasCA.pem > /srv/hasCA-chain.pem

openssl verify -CAfile hasCA-chain.pem /serv/destek.pem
cat /srv/hasICA.pem /srv/hasCA.pem > /srv/hasCA-chain.pem
````
https://propellered.com/2017/11/13/cfssl_setting_up/
