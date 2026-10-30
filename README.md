<img width="1024" height="572" alt="image" src="https://github.com/user-attachments/assets/c1541f49-7512-48e5-b977-763c08a3e528" />

Celestia Mocha Testnet çok uzun zamandır devam ediyor ve Mainnet sonrası da durmadan çalışmaya devam etti. Celestia ekibi geliştirmelerini bu ağ üzerinden sürdürüyor. Ağ şu an mocha-5 üzerinde çalışıyor (mocha-4'teki validatorler taşınmadı, mocha-5'te yeniden oluşturulması gerekiyor). Aşağıda oluşturduğum scriptin kodları var. Çalıştırdığınızda kurmak istediğiniz node'u seçenekler arasından seçip çok kısa sürede kurulmasını sağlayabilirsiniz. Validator, Fibre, Bridge ve Light Node kurulumlarının yanı sıra diğer işlemler için de seçenekler bulunmaktadır. Script güncel sürümlere göre hazırlanmıştır (celestia-app v10.5.0-mocha, celestia-node v0.34.4-mocha).

NOT: Full Storage Node tipi celestia-node'dan kaldırıldı. Bütün veriyi tutmak isteyenler Bridge Node'u --archival ile çalıştırabilir.

```
curl -s https://raw.githubusercontent.com/okannako/celestiamochascript/main/nodescript.sh > nodescript.sh && chmod +x nodescript.sh && ./nodescript.sh
```

### bbr Aktif Hale Getirmek (Mutlaka Yapın)
- Validator kurulumunda script bunu otomatik yapar. Bridge veya Light Node kurduysanız ya da kontrol etmek isterseniz aşağıdaki kodları girebilirsiniz.
```
cd $HOME/celestia-app
make bbr-enable
make bbr-check
```

- Eğer yukarıdaki kodlarda hata alırsanız aşağıdaki kodla aktif hale getirebilirsiniz.
```
sudo modprobe tcp_bbr
echo "net.core.default_qdisc=fq" | sudo tee -a /etc/sysctl.conf
echo "net.ipv4.tcp_congestion_control=bbr" | sudo tee -a /etc/sysctl.conf
sudo sysctl -p
```

- Aktiflik kontrolünü aşağıdaki kodla yaptığınızda sonuç olarak `bbr` vermelidir.
```
sysctl net.ipv4.tcp_congestion_control | awk '{print $3}'
```

Kurulum sırasında veya sonrasında bir şey sormak isterseniz bana Telegram, Mail ve Discord yoluyla ulaşabilirsiniz.
