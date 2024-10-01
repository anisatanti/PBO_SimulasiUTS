# **SIMULASI UTS PBO SOAL NOMOR 6**
___
## **Berikut Langkah-langkah membuat Crud dengan Java Swing untuk entitas Buku dengan atribut: ISBN, Judul Buku, Tahun Terbit.**
**1. Buat project baru** pada Netbeans namun unchecklist pada Create Main Class.

**2. Klik kanan pada default package kemudian pilih New, klik JFrame Form lalu beri nama FrameBuku.**

**3. Buat Kelas DbUtils** dengan cara klik kanan pada default package kemudian pilih New, klik Java Class. Kelas DbUtils ini berfungsi mengonversi objek ResultSet dari database menjadi TableModel agar dapat ditampilkan pada JTable di GUI java Swing. Dengan demikian, kita dapat meneruskan data menggunakan object ResultSet ke Jtable tanpa menulis kodenya secara manual.

```import java.sql.ResultSet;
import java.sql.ResultSetMetaData;
import java.util.Vector;
import javax.swing.table.DefaultTableModel;
import javax.swing.table.TableModel;

public class DbUtils {

    public static TableModel resultSetToTableModel(ResultSet rs) {
        try {
            ResultSetMetaData metaData = rs.getMetaData();
            int numberOfColumns = metaData.getColumnCount();
            Vector columnNames = new Vector();

            // Get the column names
            for (int column = 0; column < numberOfColumns; column++) {
                columnNames.addElement(metaData.getColumnLabel(column + 1));
            }
            // Get all rows.
            Vector rows = new Vector();
            while (rs.next()) {
                Vector newRow = new Vector();

                for (int i = 1; i <= numberOfColumns; i++) {
                    newRow.addElement(rs.getObject(i));
                }
                rows.addElement(newRow);
            }
            return new DefaultTableModel(rows, columnNames);
        } catch (Exception e) {
            e.printStackTrace();
            return null;
        }
    }
}
```
**4. Membuat Database berisi tabel Buku** pada PostgreSQL dengan rincian sebagai berikut. ISBN dengan tipe data char(13) dan set sebagai primary key, Judul_Buku dengan tipe data Varchar(100), Tahun_Terbit dengan tipe data int, serta Penerbit dengan tipe data Varchar(50).
