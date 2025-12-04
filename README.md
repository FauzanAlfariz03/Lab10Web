# Pratikum 10: PHP OOP

Nama: Fauzan Alfariz

NIM: 312410620

Kelas: TI.24.A4

## Mobile.php
```php
<?php
class Mobil {
    private $warna;
    private $merk;
    private $harga;

    public function __construct() {
        $this->warna = "Biru";
        $this->merk = "BMW";
        $this->harga = "10000000";
    }

    public function gantiWarna($warnaBaru) {
        $this->warna = $warnaBaru;
    }

    public function tampilWarna() {
        echo "Warna mobil: " . $this->warna;
    }
}

$a = new Mobil();
$b = new Mobil();

echo "<b>Mobil pertama</b><br>";
$a->tampilWarna();
echo "<br>Ganti warna menjadi Merah<br>";
$a->gantiWarna("Merah");
$a->tampilWarna();

echo "<br><br><b>Mobil kedua</b><br>";
$b->gantiWarna("Hijau");
$b->tampilWarna();
?>
```

<img width="1233" height="528" alt="image" src="https://github.com/user-attachments/assets/14f15d98-2b51-4d2e-b4b5-1ae58dcb5f61" />


## Form.php
```php
<?php
class Form {
    private $fields = array();
    private $action;
    private $submit = "Submit";
    private $jumField = 0;

    public function __construct($action, $submit) {
        $this->action = $action;
        $this->submit = $submit;
    }

    public function addField($name, $label) {
        $this->fields[$this->jumField]['name'] = $name;
        $this->fields[$this->jumField]['label'] = $label;
        $this->jumField++;
    }

    public function displayForm() {
        echo "<form action='$this->action' method='POST'>";
        echo "<table>";

        for ($i = 0; $i < count($this->fields); $i++) {
            echo "<tr><td>".$this->fields[$i]['label']."</td>";
            echo "<td><input type='text' name='".$this->fields[$i]['name']."'></td></tr>";
        }

        echo "<tr><td colspan='2'>";
        echo "<input type='submit' value='$this->submit'>";
        echo "</td></tr>";

        echo "</table>";
        echo "</form>";
    }
}
?>
```

## Form_input.php
```php
<?php
include "form.php";

echo "<h2>Input Data Mahasiswa</h2>";

$form = new Form("proses.php", "Simpan Data");

$form->addField("nim", "NIM");
$form->addField("nama", "Nama");
$form->addField("alamat", "Alamat");

$form->displayForm();
?>
```

<img width="944" height="489" alt="image" src="https://github.com/user-attachments/assets/4d301817-3923-4181-a0e4-6cef581523f7" />


## Database.php
```php
<?php
class Database {
    protected $host;
    protected $user;
    protected $password;
    protected $db_name;
    protected $conn;

    public function __construct() {
        $this->getConfig();
        $this->conn = new mysqli($this->host, $this->user, $this->password, $this->db_name);

        if ($this->conn->connect_error) {
            die("Connection failed : " . $this->conn->connect_error);
        }
    }

    private function getConfig() {
        include_once "config.php";
        $this->host = $config['host'];
        $this->user = $config['username'];
        $this->password = $config['password'];
        $this->db_name = $config['db_name'];
    }

    public function query($sql) {
        return $this->conn->query($sql);
    }

    public function insert($table, $data) {
        $columns = implode(",", array_keys($data));
        $values  = "'" . implode("','", array_values($data)) . "'";

        $sql = "INSERT INTO $table ($columns) VALUES ($values)";
        return $this->conn->query($sql);
    }
}
?>
```

Pertanyaan dan Tugas

<img width="889" height="105" alt="image" src="https://github.com/user-attachments/assets/024aabf3-fe03-40c9-b1d9-e6410a4c2fee" />

## Beriku Hasil:

<img width="950" height="661" alt="image" src="https://github.com/user-attachments/assets/3f94b30f-9660-42bc-b07c-a0526e31ede3" />


