# Rangkuman TBA
#### opensourced github.com/satraul/rangkuman\-tba.git

## PDA
### Definisi
Push Down Automata (PDA) adalah Finite State Machine yang dilengkapi dengan sebuah unlimited stack. 
PDA M adalah tupel K (states), Σ (input), Γ (stack), ∆ (transisi), s (start), A (accept). Notasi ∆:
(img)
### Komputasi
- Jika C adalah komputasi yang dilakukan oleh M pada input w ∈ Σ\*
	- C: accepting computation iff C = (s, w, ε)├M\* (q, ε, ε) untuk suatu q ∈ A
	- C: rejecting computation iff C = (s, w, ε)├M\* (q, w’, ⍺) di mana C bukan accepting computation dan tidak ada move yang mungkin dari (q,w’, ⍺), dengan kata lain konfigurasi halt.
- M menerima (accept) w iff paling tidak satu komputasi menerimanya. M menolak (reject) w iff semua komputasi menolaknya.
- Bahasa yang diterima oleh M, notasi L(M), adalah himpunan semua string w yang diterima oleh M
### Grammar -> PDA
Diberikan suatu CFG G = (V, Σ, R, S), terdapat sebuah PDA M sehingga L(M) = L(G)
#### Topdown
Mulai dari S, menerapkan sejumlah rule R, dan memeriksa apakah ada derivasi dari G ke w
(img)
#### Bottom-up
Mulai dari w, menerapkan sejumlah rule R backward, dan memeriksa apakah S dicapai
(img)
## CFL
### Detriministik CFL
- Sementara Bahasa Reguler memiliki sifat closure pada operasi komplemen, irisan dan difference,
	- CFL tidak memiliki sifat closure tersebut.
- Ingat bahwa suatu PDA M deterministik jika
	- ΔM tidak memiliki lebih dari satu pilihan transisi dari setiap konfigurasi.
	- Jika q accepting state dalam M, maka tidak ada transisi (q, ε, ε), (p, a)).
- Bahasa L adalah CFL deterministik iff L$ dapat diterima oleh PDA deterministik.
	- L$ = \{w$ : w ∈ L, dan $ adalah simbol end-of-string}
### Teorema Pumping untuk CFL
wkwkkw
### Sifat Closure CFL
- CFL Closure dalam operasi union, konkatenasi, Kleene Star, Reverse, dan letter substitution 
	- Sifat closure **op** adalah “Jika L1 **op** L2 adalah CFL jika L1 dan L2 keduanya CFL”
- CFL tidak closure dalam operasi irisan, komplemen, dan different 
	- Tetapi CFL closure dalam operasi irisan/different dengan bahasa reguler 
### Ogden’s Lemma
Untuk buktiin bahwa L adalah context-free
(img)
## Turing Machine
### Definisi
- Bayangkan suatu FSM yang dilengkapi storage berbentuk tape 
	- Tape berbentuk linear, setiap posisi, atau square, terurut dari kiri ke kanan, 
	- Setiap posisi dapat menyimpan satu simbol tape atau kosong (), 
	- Kapasitas (panjang tape) tak berhingga (tidak berujung baik di kiri maupun di kanan). 
- Read/write dilakukan melalui sebuah head
	- Head bergerak secara sikuensial dari satu posisi ke posisi berikutnya (arah R)/sebelumnya (arah L) 
### Komputasi
- Komputasi dilakukan menurut current state, current data tape (pada head), untuk bertransisi ke next-state, meng-update isi tape (pada head), arah pemindahan head.
- Dengan tape, input string bisa diasumsikan sudah langsung ditaruh di dalam tape, sehingga mesin segera bekerja pada tape.
- Konvensi konfigurasi awal: head berada di paling kiri tape sebelum string input.
### Halting, Crash, Forever Loop
- Mesinberhentijika:
	- Mencapai status halt (status khusus untuk menyatakan mesin berhenti).
	- Terpaksa berhenti (crash) karena transisi untuk konfigurasi saat ini (status dan isi tape pada head) tidak terdefinisi.
- Mesin bisa tidak pernah berhenti (karena forever-loop)
	- Tidak dapat mencapai halt maupun crash.
	- Karena kesalahan logika dalam pendefinisian transisi atau karena nature of its related problem sendiri (tidak ada mesin ekivalen yang bisa halt/crash)
### Notasi Makro
(img)
(img)
### Varian-varian
- Mesin Turing Multitape
	- Perbedaannya:
		- adanya tape sebanyak k buah,
		- masing-masing memiliki satu head sendiri,
		- konfigurasi mesin terdiri atas status current, isi dari tape-tape tsb, dan posisi head setiap tape
		- Transisi merupakan fungsi 
			- ((K-H) ⨯ Γ1 ⨯ … ⨯ Γk) -> (K ⨯ Γ1 ⨯ \{->,<-, ↑} ⨯ ... ⨯ Γk ⨯ \{->,<-, ↑}
			- ↑ (atau S) artinya tetap
	- Manfaat: S sebagai tempat sementara, contoh: operasi duplikasi string 
- NDTM
- Mesin Turing One-way
### Mesin Turing Universal (UTM)
(img)
DansGame Explain?
(img)
## D&SD
### Decidable
- Suatu bahasa dikatakan Decidable (D) jika ada mesin Turing yang selalu dapat menerima setiap string dari bahasa itu dan selalu dapat menolak setiap string yang bukan dari bahasa tersebut.
- Apabila mesin Turing Turing memiliki Halt-yes dan Halt-no, maka Mesin Turing dikatakan menerima string input apabila mesin berhenti di Halt -yes, sementara dikatakan menolak apabila mesin berhenti di Halt-no. 
- Apabila mesin Turing hanya memiliki Halt, maka Mesin Turing dikatakan menerima string input apabila mencapai Halt, sementara dikatakan menolak apabila tidak mencapai Halt (alias Chrash).
- TM M **decide** L, **iff**: ∀w ∈ Σ\*:
	- Jika w ∈ L maka M menerima w (halt di hy)
	- ika w ∉ L maka M **menolak** w (halt di hn)
- L adalah decidable (L ∈ D) iff terdapat TM M yang decide L. 
- Setiap CFL adalah decidable karena setiap PDA dapat disimulasikan oleh mesin Turing dengan memperlakukan bagian tertentu tape menggantikan seperti stack. Jika PDA nondeterministik maka sederhananya mesin Turing juga dibuat nondeterministik. Termasuk juga adalah setiap bahasa reguler, Finite State Machine untuk bahasa itu dapat disimulasikan oleh mesin Turing. 
- CFL proper subset dari D apabila ada bahasa D yang bukan CFL. Kita mengetahui dari contoh-contoh pada bagian sebelumnya bahasa AnBnCn dan juga bahasa WW, adalah bukan CFL tetapi dapat di-decide oleh mesin Turing. Jadi memang CFL proper subset dari D. 
### Definisi SD
- Suatu bahasa dikatakan Semidecidable (SD) jika ada mesin Turing yang selalu dapat menerima setiap string dari bahasa tersebut, sementara untuk string lainnya “tidak menerima”.
- Tidak menerima tidak harus menolak (berhenti di Halt-no atau crash) tetapi juga karena tidak mesin terus berkomputasi tanpa henti (infinite loop). 
### Relasi Reguler ⊂ CFL ⊂ D ⊂ SD
### Halting Problem (H)
### Sifat Closure D
- D Closure pada Komplemen 
- SD Tidak Closure pada Komplemen 
- “L dan ￢L keduanya SD”, berarti juga “L dan ￢L keduanya D” 
- Jika L adalah D, maka L dan ￢L adalah SD. Bukti: L adalah D, maka ￢L adalah D. Karena keduanya adalah D maka keduanya adalah juga SD.

### Non-halting Problem (￢H)
- Jika H adalah \{<M,w>: Mesin Turing M halt pada string input w} maka ￢H adalah \{<M,w>: Mesin Turing M tidak halt pada string input w.}
- Jika UTM menjalankan <M,w> ∈ ￢H, maka mesin bisa jadi infinite loop (“tanpa berakhir dengan memberikan keputusan”). Maka ￢H bukan SD karena tidak memenuhi definisi mengenai bahasa-bahasa SD.
### Mesin Enumerator
- Mesin Enumerator L adalah mesin Turing yang dapat menghasilkan output berupa enumerasi secara string-string dari bahasa L.
- Secara umum enumerasi tidak harus secara proper-order, bisa juga secara sembarang/acak.
- Mesin Turing enumerator dapat didefinisikan dengan adanya notasi makro P untuk “mengirimkan/mencetak” isi tape yang telah berisi string.
(img)
- Jika L finite maka mesin suatu saat harus halt, jika L infinite maka M akan beriterasi tanpa pernah halt karena terus-menerus akan berkomputasi menghasilkan string berikutnya.
### String Generator
- Mesin enumerator Σ\* dapat digunakan sebagai string generator Σ\* (SG Σ\*) untuk enumerator bahasa-bahasa lain. Misalnya: String Enumerator WW = \{ww : w ∈ Σ\*}
- Enumerator M untuk WW bekerja sbb.
	1. Mesin M memanggil SG Σ\*
	2. setiap saat P dijalankan oleh SG, string yang dihasilkan dalam tape diperiksa oleh TM Mww (mesin yang mengenali WW), saat Mww halt di hy maka M menjalankan P.
	3. Ulangi mulai langkah 1.
### Dovetailing
- Untuk menghindarkan M terjebak dalam infinite loop saat memeriksa suatu string w ∈ L.
- Enumerator menerapkan stepping counter dalam pada komputasi ML dengan satu step adalah satu transisi dalam ML.
- Selain itu beberapa instant ML dijalankan sekaligus untuk memeriksa sejumlah string. Jika SG menghasilkan w1, w2, w3, … pada step pertama komputasi untuk w1, pada step kedua komputasi untuk w1, dan w2 (jika untuk w1 belum halt/crash), step ketiga untuk w1, w2, w3 (jika untuk w1 dan w2 belum halt/crash), dan seterusnya.
- Contoh: SG \{a,b}\* menghasilkan ε, a, b, aa, ab, ba, bb, dst ... maka dovetailing menyebabkan komputasi paralel sebagai berikut.
- Dapat disimpulkan:
	- Bahasa L disebut turing enumerable jika dapat dienumerasikan (baik secara proper-order maupun acak)
	- Bahasa L disebut turing enumerable secara proper-order jika dapat dienumerasikan secara proper-order
	- Suatu bahasa L adalah SD iff L turing enumerable.
	- Suatu bahasa L adalah D iff L turing enumerabel secara proper-order
### Metode reduksi -> mapping reduction
sumpah w gatau