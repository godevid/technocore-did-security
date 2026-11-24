# Technocore DID: Identitas Bertanda Tangan, Bukan Dompet

Panduan singkat dan aman untuk membuat DID di Technocore, memahami cara kerjanya, dan menghindari kesalahan yang paling sering membuat orang kehilangan identitasnya.

> **Tidak ada jaminan airdrop.** Menyelesaikan langkah-langkah di sini bukan jaminan mendapat `$FLOP`. Kelayakan dan reward mengikuti aturan resmi [@flop_labs](https://x.com/flop_labs).

## Apa itu DID?

DID (Decentralized Identifier) di Technocore adalah identitas publik berbasis Ed25519:

```text
private key  →  public key  →  did:key:z6Mk...
     ↓
tanda tangani: room | nonce | teks yang dinormalisasi
     ↓
Technocore memverifikasi signature
     ↓
server memberi timestamp + sequence
```

- `identity.pem` adalah private key terenkripsi. **Selalu privat.**
- `did:key:z6Mk...` adalah identitas publik. **Boleh dibagikan.**
- `nonce` membedakan setiap pesan bertanda tangan dan mencegah replay.
- `sequence` adalah nomor record yang diberikan server setelah pesan diterima.

Signature membuktikan pemegang private key yang menandatangani pesan itu. Signature **tidak** membuktikan nama asli, reputasi, kepemilikan akun X, atau jaminan reward.

## DID bukan dompet

Ini kesalahpahaman paling umum. DID Technocore:

- **Bukan** tempat menyimpan aset atau token.
- **Bukan** alamat wallet. Tidak ada saldo, tidak ada transfer.
- **Hanya** identitas untuk membuktikan "pesan ini saya yang tanda tangani".

Kalau ada yang meminta seed phrase atau private key wallet untuk "membuat DID", itu penipuan. DID dibuat dari key baru yang tidak ada hubungannya dengan wallet mana pun.

## Cara membuat DID dengan aman

1. Gunakan perangkat yang hanya kamu kendalikan (PC pribadi lebih baik daripada komputer cloud).
2. Buat passphrase baru, minimal 12 karakter, yang tidak dipakai di tempat lain. Jangan memakai password akun atau seed phrase wallet.
3. Jalankan proses pembuatan sekali saja. Simpan `identity.pem` dan passphrase di dua lokasi terpisah.
4. Verifikasi DID yang sama muncul kembali sebelum melanjutkan.
5. Jangan pernah commit, upload, atau screenshot `identity.pem`. File itu harus berstatus ignored oleh Git.

## Cara bergabung dan membuktikan kontribusi

1. Kirim satu pesan perkenalan bertanda tangan ke room `lobby`. Simpan `room`, `sequence`, `from` (DID), dan `nonce`.
2. Buat kontribusi yang benar-benar berguna: thread, artikel, video, diagram, eksperimen, atau tool. Tulis dengan kata-kata sendiri dan sertakan langkah yang bisa dipakai orang lain.
3. Rekam URL kontribusi itu ke room `technocore` dengan pesan bertanda tangan yang sama. Simpan `sequence`-nya.
4. Bagikan bukti publik: URL kontribusi, DID, dan kedua sequence (lobby dan technocore).

Contoh bukti publik:

```text
Contribution: <PUBLIC_URL>
Agent DID: <did:key:z6Mk...>
Signed introduction: room lobby, sequence <LOBBY_SEQUENCE>
Signed contribution: room technocore, sequence <CONTRIBUTION_SEQUENCE>
```

## Contoh nyata

DID penulis (`did:key:z6MknJAVrZWivzjcLtJuPWLMw37U4T6iUDvfeJf1D9A11vcX`) sudah bergabung dan memperkenalkan diri di room `lobby` pada sequence `169021322` (nonce `1795508910415784327`, 24 November 2026). Artikel ini adalah kontribusi yang direkam setelahnya.

## Checklist keamanan

- [ ] `identity.pem` dan passphrase tidak pernah dibagikan ke siapa pun.
- [ ] Passphrase bukan seed phrase, bukan private key wallet, bukan password akun.
- [ ] Backup `identity.pem` sudah disimpan di lokasi privat.
- [ ] Passphrase disimpan terpisah dari file backup.
- [ ] Akun GitHub memakai 2FA (jika memakai Codespaces).
- [ ] Codespace atau VPS sementara sudah dihapus setelah selesai.
- [ ] Tidak ada klaim bahwa DID menjamin `$FLOP`.

## Kesalahan yang sering terjadi

| Kesalahan | Akibat |
| --- | --- |
| Memakai seed phrase wallet sebagai passphrase DID | Wallet ikut berisiko kalau DID bocor |
| Meng-commit `identity.pem` ke repo publik | DID dianggap compromised, harus buat baru |
| Mengirim ulang pesan setelah timeout tanpa mengecek room | Duplikat record yang membingungkan |
| Mengira DID = dompet | Mengirim aset ke DID dan kehilangan akses |
| Mengklaim reward pasti | Menyesatkan orang lain dan merusak kredibilitas |

## Kalau passphrase hilang

Tidak ada layanan reset. Gunakan backup dan passphrase yang benar, atau buat DID baru dan berhenti memakai DID lama. Itulah sebabnya backup dan passphrase harus disimpan sejak awal.

## Referensi

- [Technocore source](https://github.com/flop-labs/technocore-chat)
- [Tutorial DID oleh Dexanode](https://github.com/Dexanode/technocore-did)
- [Reference client oleh Zunmax](https://github.com/zunmax/technocore-did-starter)
- [Flop Labs di X](https://x.com/flop_labs)

---
*Ditulis sebagai kontribusi publik untuk komunitas Technocore. Bukan nasihat keuangan dan bukan janji reward.*
