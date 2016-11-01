#Kelas Git BlankOn
	Jumat, 14 Oktober 2016 
	Pemateri: @Herpiko Dwi Aguno 
	Pencatat: @Raviyanto Ahmad

***


####Memasang dan Mengonfigurasi Git
Pertama-tama kita pasang Git di komputer kita dan kita konfigurasi.

	$ sudo apt install git
	$ git config --global user.name "Nama saya"
	$ git config --global user.email "email@saya.com"
	
Di sini saya sebagai pencatat mengisi "**Nama saya**" dengan "**Raviyanto Ahmad**" dan "email@saya.com" dengan "raviyanto@gmail.com".
	
Pemasangan dan konfigurasi Git tersebut kita cek.

	$ git --version
	$ git config user.name
	$ git config user.email
	
Versi Git yang saya instal adalah versi 2.7.4. Hasil perintah **git config user.name** adalah **Raviyanto Ahmad**. Hasil perintah **git config user.email** adalah raviyanto@gmail.com.
	
####Menginisiasi Proyek Baru
Sekarang kita coba menginisiasi sebuah proyek baru.

	$ mkdir puisi
	$ cd puisi
	$ git init
	
Hasil perintah **git init** adalah **Initialized empty Git repository in /home/raviyanto/puisi/.git/.** Di direktori **puisi **ada direktori tersembunyi **.git**.

####Melihat Status Proyek

Mari kita lihat status proyek kita.

	$ git status
	On branch master
	
	Initial commit
	
	nothing to commit (create/copy files and use "git add" to track)
	
Perintah **git status**  digunakan untuk melihat status/kondisi direktori kerja kita. Apakah ada berkas yang sudah dimodifikasi dan belum dikomit? Apakah ada yang tertinggal? Apakah ada berkas baru? Semua bisa dicek dari sini.

Hasil perintah **git status** di atas menunjukkan tidak  ada komit baru, yang ada komit awal atau *initial commit*.

Kita coba membuat berkas baru.

	$ touch puisi1.txt

Sunting berkas tersebut pakai editor favorit masing-masing.

	$ nano puisi1.txt

Tulis satu baris saja.

	oh engkau yang nun jauh di sana

Simpan dan keluar dari editor. Kemudian jalankan **git status**.

	$ git status
	On branch master
		
	Initial commit
		
	Untracked files:
	    (use "git add <file>..." to include in what will be committed)
		
		      puisi1.txt
		
	nothing added to commit but untracked files present (use "git add" to track)

Berkas **puisi1.txt** belum aman. Nah, di sini saya akan jelaskan alur Git. Alur Git itu ada tiga:
1. Direktori kerja (*working directory*)
2. Tempat penampungan (*stage*)
3. Kepala versi (*head*)

![Alur Git](/images/trees.png) 


####Memindahkan Direktori ke Tempat Penampungan
Sekarang kita masih di direktori kerja, belum masuk tempat penampungan. Mari kita pindah ke tempat penampungan.

	$ git add puisi1.txt
	
Perintah tersebut membawa kita ke tempat penampungan. Contoh perintah lain.

	$ git add .
	$ git add --all
	$ git add *.txt

Kita lihat status berkas dengan perintah **git status**.

	$ git status
	On branch master
	
	Initial commit
	
	Changes to be committed:
	  (use "git rm --cached <file>..." to unstage)
	
		new file:   puisi1.txt

####Mengesahkan Direktori
Nah, berkas sudah berada di penampungan. Tugas kita selanjutnya adalah melakukan komit atau pengesahan.

	$ git commit -m "pesan komit"
	You need a passphrase to unlock the secret key for
	user: "Raviyanto Ahmad <raviyanto@gmail.com>"
	4096-bit RSA key, ID 7EC72E69, created 2016-10-18
	
	[master (root-commit) fea7aa1] pesan komit
	 1 file changed, 1 insertion(+)
	 create mode 100644 puisi1.txt

Sekarang kita sudah pindah ke kepala versi (*head*). Mengapa di sini perlu ada tempat penampungan (*stage*). Mengapa tidak langsung pindah ke kepala versi? Tujuannya adalah memudahkan kita memanajemen berkas yang lebih dari satu. Ada kalanya kita menyunting beberapa berkas untuk satu komit. Tempat penampungan mempermudah pekerjaan kita.

####Melihat Daftar Pengesahan
Sekarang kita memiliki satu pengesahan (komit). Kita dapat melihat daftarnya dengan perintah **git log**.

	$ git log
	commit fea7aa1719789464aac29aa7de875982194d89a3
	Author: Raviyanto Ahmad <raviyanto@gmail.com>
	Date:   Sun Oct 23 11:02:18 2016 +0700
	
	    pesan komit

Mari kita sunting berkas puisi1.txt. Simpan, taruh di penampungan, lalu sahkan. Kita lihat daftar pengesahan yang kita lakukan.

	$ git log
	commit 5676c71d12bfac1522a56cb6f2b05a1a3ca89e8a
	Author: Raviyanto Ahmad <raviyanto@gmail.com>
	Date:   Sun Oct 23 11:56:07 2016 +0700
	
	    tambah satu baris
	
	commit fea7aa1719789464aac29aa7de875982194d89a3
	Author: Raviyanto Ahmad <raviyanto@gmail.com>
	Date:   Sun Oct 23 11:02:18 2016 +0700
	
	    pesan komit

Setiap pengesahan punya nomor identitas. Pengesahan pertama bernomor **fea7**. Pengesahan kedua bernomor **5676**.

####Berpindah Pengesahan
Kita ingin pindah ke pengesahan pertama. 

	$ git checkhout fea7
	Note: checking out 'fea7'.
	
	You are in 'detached HEAD' state. You can look around, make experimental changes and commit them, and you can discard any commits you make in this state without impacting any branches by performing another checkout.
	If you want to create a new branch to retain commits you create, you may do so (now or later) by using -b with the checkout command again. Example:
	
	  git checkout -b <new-branch-name>
	
	HEAD is now at fea7aa1... pesan komit

Artinya, kita tidak berada di cabang mana pun. Status kepala versi kita mengambang, lepas dari cabang mana pun. Mari kita cek cabang yang ada.

	$ git branch
	* (HEAD detached at fea7aa1)
	  master
  
Sebelumnya kita berada di cabang **master**. Setelah berpindah ke pengesahan pertama, kita berada di cabang yang mengambang. Ini tidak aman. Kita perlu membuat cabang yang sah. Perintah **checkout** tidak hanya berfungsi berpindah pengesahan atau pencabangan, tapi juga membuat pencabangan baru.

	$ git checkout -b pesanawal

Artinya, dari pengesahan tersebut, saya membuat pencabangan baru. Nama cabangnya **pesanawal**. Di situ ada opsi -b (*branch*). Sekarang kita lihat daftar cabang lagi.

	$ git branch
	   master
	* pesanawal
	
Kita berada di cabang **pesanawal**. Dari mana kita tahu? Ada tanda bintang (*) di depannya.

Oke, kita lanjut. Cabang-cabang ini bisa kita gabung (*merge*). Kita sekarang punya dua cabang, yaitu **master** dan **pesanawal**. Kita kembali ke cabang **master**.

	$ git checkout master
  
 Setelah berada di **master** dan berada di pengesahan terakhir, kita buat cabang baru. Namanya **pesankedua**.
  
	  $ git checkout -b pesankedua
  
 Kedua cabang ini--**master **dan **pesankedua**--statusnya sama, pengesahannya sama. Anggap saja **master** adalah cabang pengembangan utama, yang resmi dan bakal rilis. Cabang **pesankedua** bersifat eksperimen. Kita membuat cabang baru supaya kita fokus di situ. Biarkan **master** bersih.
 
 Sekarang kita berada di cabang **pesankedua**. Mari kita sunting puisinya lalu simpan.
 
	$ git status
	On branch pesankedua
	Changes not staged for commit:
	    (use "git add <file>..." to update what will be committed)
	    (use "git checkout -- <file>..." to discard changes in working directory)
	
		      modified:   puisi1.txt
	
	no changes added to commit (use "git add" and/or "git commit -a")

  Statusnya belum aman karena belum masuk ke penampungan dan pengesahan.

	$ git add --all
	$ git commit -m "pesan kedua"
	$ git log
	
Sekarang kita punya tiga pengesahan.

	commit 6a654ef35830d3eb35b3427c85a7de6a96d1e2ae
	Author: Raviyanto Ahmad <raviyanto@gmail.com>
	Date:   Sun Oct 30 21:20:39 2016 +0700
	
	    pesan kedua
	
	commit 5676c71d12bfac1522a56cb6f2b05a1a3ca89e8a
	Author: Raviyanto Ahmad <raviyanto@gmail.com>
	Date:   Sun Oct 23 11:56:07 2016 +0700
	
	    tambah satu baris
	
	commit fea7aa1719789464aac29aa7de875982194d89a3
	Author: Raviyanto Ahmad <raviyanto@gmail.com>
	Date:   Sun Oct 23 11:02:18 2016 +0700
	
	    pesan komit
	
Pada cabang **pesankedua** kita punya tiga pengesahan. Ini lebih  baru daripada cabang **master**. Nah, ceritanya kita ingin menggabungkan kedua cabang ini. Kita bawa fitur baru di cabang **pesankedua** ke **master**.

Sebelum kita gabungkan, ada baiknya kita cek dulu.

	$ git diff master
	
	diff --git a/puisi1.txt b/puisi1.txt
	index 8466d82..23ff8ff 100644
	--- a/puisi1.txt
	+++ b/puisi1.txt
	@@ -1,2 +1,3 @@
	 oh engkau yang nun jauh di sana
	 datanglah ke sini bersama angin
	+bercengkerama di pantai cita


Yang bertanda **+** dan** -** menunjukkan perubahan. Tanda **+** artinya ada penambahan baris. Tanda **-** artinya ada pengurangan baris. Sekarang kita mau gabung **pesankedua** ke **master.**

	$ git checkout master
	$ git merge pesankedua

Perintah **git merge** tersebut hasilnya sebagai berikut.

	Updating 5676c71..6a654ef
	Fast-forward
	 puisi1.txt | 1 +
	 1 file changed, 1 insertion(+)






 