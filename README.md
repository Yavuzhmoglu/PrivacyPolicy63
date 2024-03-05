# PrivacyPolicy


**Terms & Conditions**

By downloading or using the app, these terms will automatically apply to you – you should make sure therefore that you read them carefully before using the app. You’re not allowed to copy or modify the app, any part of the app, or our trademarks in any way. You’re not allowed to attempt to extract the source code of the app, and you also shouldn’t try to translate the app into other languages or make derivative versions. The app itself, and all the trademarks, copyright, database rights, and other intellectual property rights related to it, still belong to Justtouch Games.

Justtouch Games is committed to ensuring that the app is as useful and efficient as possible. For that reason, we reserve the right to make changes to the app or to charge for its services, at any time and for any reason. We will never charge you for the app or its services without making it very clear to you exactly what you’re paying for.

The Stickers 2D app stores and processes personal data that you have provided to us, to provide my Service. It’s your responsibility to keep your phone and access to the app secure. We therefore recommend that you do not jailbreak or root your phone, which is the process of removing software restrictions and limitations imposed by the official operating system of your device. It could make your phone vulnerable to malware/viruses/malicious programs, compromise your phone’s security features and it could mean that the Stickers 2D app won’t work properly or at all.

The app does use third-party services that declare their Terms and Conditions.

Link to Terms and Conditions of third-party service providers used by the app

*   [Google Play Services](https://policies.google.com/terms)
*   [AdMob](https://developers.google.com/admob/terms)
*   [Google Analytics for Firebase](https://firebase.google.com/terms/analytics)
*   [Firebase Crashlytics](https://firebase.google.com/terms/crashlytics)
*   [Unity](https://unity3d.com/legal/terms-of-service)

You should be aware that there are certain things that Justtouch Games will not take responsibility for. Certain functions of the app will require the app to have an active internet connection. The connection can be Wi-Fi or provided by your mobile network provider, but Justtouch Games cannot take responsibility for the app not working at full functionality if you don’t have access to Wi-Fi, and you don’t have any of your data allowance left.

If you’re using the app outside of an area with Wi-Fi, you should remember that the terms of the agreement with your mobile network provider will still apply. As a result, you may be charged by your mobile provider for the cost of data for the duration of the connection while accessing the app, or other third-party charges. In using the app, you’re accepting responsibility for any such charges, including roaming data charges if you use the app outside of your home territory (i.e. region or country) without turning off data roaming. If you are not the bill payer for the device on which you’re using the app, please be aware that we assume that you have received permission from the bill payer for using the app.

Along the same lines, Justtouch Games cannot always take responsibility for the way you use the app i.e. You need to make sure that your device stays charged – if it runs out of battery and you can’t turn it on to avail the Service, Justtouch Games cannot accept responsibility.

With respect to Justtouch Games’s responsibility for your use of the app, when you’re using the app, it’s important to bear in mind that although we endeavor to ensure that it is updated and correct at all times, we do rely on third parties to provide information to us so that we can make it available to you. Justtouch Games accepts no liability for any loss, direct or indirect, you experience as a result of relying wholly on this functionality of the app.

At some point, we may wish to update the app. The app is currently available on Android & iOS – the requirements for the both systems(and for any additional systems we decide to extend the availability of the app to) may change, and you’ll need to download the updates if you want to keep using the app. Justtouch Games does not promise that it will always update the app so that it is relevant to you and/or works with the Android & iOS version that you have installed on your device. However, you promise to always accept updates to the application when offered to you, We may also wish to stop providing the app, and may terminate use of it at any time without giving notice of termination to you. Unless we tell you otherwise, upon any termination, (a) the rights and licenses granted to you in these terms will end; (b) you must stop using the app, and (if needed) delete it from your device.

**Changes to This Terms and Conditions**

I may update our Terms and Conditions from time to time. Thus, you are advised to review this page periodically for any changes. I will notify you of any changes by posting the new Terms and Conditions on this page.

These terms and conditions are effective as of 2022-02-18

**Contact Us**

If you have any questions or suggestions about my Terms and Conditions, do not hesitate to contact me at justtouchinfo@gmail.com.





using System;
using System.Data;
using System.Data.SqlClient;
using System.Drawing;
using System.Windows.Forms;
using Zuby.ADGV;

namespace Veri
{
    public partial class Form1 : Form
    {
        
        private string connectionString = "Data Source=DESKTOP-OPQQL1L\\SQLEXPRESS;Initial Catalog=DenemeExcelVT;Integrated Security=True";
        private SqlDataAdapter dataAdapter;
        private DataTable dataTable;
//        private Zuby.ADGV.AdvancedDataGridView advancedDataGridView;

        public Form1()
        {
            InitializeComponent();

            // AdvancedDataGridView kontrolünü oluştur
           // advancedDataGridView1 = new Zuby.ADGV.AdvancedDataGridView();
            advancedDataGridView1.Dock = DockStyle.Fill;

            // Forma AdvancedDataGridView kontrolünü ekle
            Controls.Add(advancedDataGridView1);

            advancedDataGridView1.ColumnHeadersVisible = true;


            advancedDataGridView1.ColumnHeadersDefaultCellStyle.BackColor = Color.LightBlue;
            advancedDataGridView1.ColumnHeadersDefaultCellStyle.ForeColor = Color.DarkBlue;
            advancedDataGridView1.AlternatingRowsDefaultCellStyle.BackColor = Color.LightGray;
            advancedDataGridView1.DefaultCellStyle.SelectionBackColor = Color.DarkOrange;
            advancedDataGridView1.DefaultCellStyle.SelectionForeColor = Color.White;
            //advancedDataGridView1.RowHeadersVisible = true;
            //advancedDataGridView1.RowHeadersWidthSizeMode = DataGridViewRowHeadersWidthSizeMode.AutoSizeToAllHeaders;
            //advancedDataGridView1.AutoSizeColumnsMode = DataGridViewAutoSizeColumnsMode.AllCells;
            //advancedDataGridView1.CellBorderStyle = DataGridViewCellBorderStyle.SingleHorizontal;
            //advancedDataGridView1.RowHeadersBorderStyle = DataGridViewHeaderBorderStyle.Single;
            //advancedDataGridView1.ColumnHeadersBorderStyle = DataGridViewHeaderBorderStyle.Single;
            //advancedDataGridView1.ColumnHeadersDefaultCellStyle.Alignment = DataGridViewContentAlignment.MiddleCenter;







        }

        private void VeriCekmeForm_Load(object sender, EventArgs e)
        {
            // Form yüklendiğinde veriyi çek ve AdvancedDataGridView kontrolüne ekle
            VeriyiCekVeGoster();

            RenklendirSutun(0, Color.Yellow);
        }

        private void VeriyiCekVeGoster()
        {
            try
            {
                // Veritabanından veriyi çek
                using (SqlConnection connection = new SqlConnection(connectionString))
                {
                    connection.Open();

                    string query = "SELECT * FROM KayitExcel";
                    dataAdapter = new SqlDataAdapter(query, connection);
                    SqlCommandBuilder commandBuilder = new SqlCommandBuilder(dataAdapter);

                    dataTable = new DataTable();
                    dataAdapter.Fill(dataTable);

                    // AdvancedDataGridView'e veriyi bağla
                    advancedDataGridView1.DataSource = dataTable;
                }
            }
            catch (Exception ex)
            {
                MessageBox.Show("Veri çekme hatası: " + ex.Message, "Hata", MessageBoxButtons.OK, MessageBoxIcon.Error);
            }
        }

        private void RenklendirSutun(int columnIndex, Color color)
        {
            if (columnIndex >= 0 && columnIndex < advancedDataGridView1.Columns.Count)
            {
                // Belirli bir sütunu renklendir
                advancedDataGridView1.Columns[columnIndex].DefaultCellStyle.BackColor = color;
            }
        }

        private void AdvancedDataGridView_RowPrePaint(object sender, DataGridViewRowPrePaintEventArgs e)
        {
            // Sadece başlık satırını renklendir
            if (e.RowIndex == -1)
            {
                advancedDataGridView1.Rows[e.RowIndex].DefaultCellStyle.BackColor = Color.LightBlue;
                advancedDataGridView1.Rows[e.RowIndex].DefaultCellStyle.ForeColor = Color.DarkBlue;
            }
        }
    }
}





---
using System;
using System.Collections.Generic;
using System.Windows.Forms;
using System.Data.SqlClient;

namespace ExcelFileProcessor.UserControls
{
    public partial class UlkelerAgaciUserControl : UserControl
    {
        private string connectionString = "Data Source=DESKTOP-OPQQL1L\\SQLEXPRESS;Initial Catalog=DenemeExcelVT;Integrated Security=True";

        public UlkelerAgaciUserControl()
        {
            InitializeComponent();
            UlkeleriGetir();
        }

        private void UlkeleriGetir()
        {
            treeViewUlkeler.Nodes.Clear();

            using (SqlConnection connection = new SqlConnection(connectionString))
            {
                connection.Open();

                string selectQuery = "SELECT Id, CountryCode FROM Country";
                SqlCommand command = new SqlCommand(selectQuery, connection);
                SqlDataReader reader = command.ExecuteReader();

                while (reader.Read())
                {
                    int ulkeId = Convert.ToInt32(reader["Id"]);
                    string ulkeKodu = reader["CountryCode"].ToString();

                    TreeNode ulkeNode = new TreeNode(ulkeKodu);
                    ulkeNode.Tag = ulkeId;

                    // Ülkenin altındaki verileri eklemek için gerekli sorguları buraya ekleyebilirsiniz.
                    // Örneğin: altındaki şehirleri çekmek için bir sorgu yapabilir ve şehirleri ulkeNode'un altına ekleyebilirsiniz.

                    treeViewUlkeler.Nodes.Add(ulkeNode);
                }

                reader.Close();
            }
        }

        private void treeViewUlkeler_AfterSelect(object sender, TreeViewEventArgs e)
        {
            // Ağaçtaki bir düğüme tıklandığında burada gerekli işlemleri yapabilirsiniz.
            // Örneğin, seçilen ülkenin altındaki verileri göstermek için gerekli sorguları yapabilirsiniz.
            // Bu kısmı projenizin gereksinimlerine göre özelleştirebilirsiniz.
            int ulkeId = (int)e.Node.Tag;
            VerileriGoster(ulkeId);
        }

        private void VerileriGoster(int ulkeId)
        {
            // Bu kısma, seçilen ülkenin altındaki verileri göstermek için gerekli sorguları ve kodları ekleyebilirsiniz.
            // Örneğin, seçilen ülkenin şehirlerini göstermek için bir sorgu yapabilir ve sonucu bir DataGridView'e bağlayabilirsiniz.
            // Bu kısmı projenizin gereksinimlerine göre özelleştirebilirsiniz.
        }
    }
}




veri  gruplama 


using System;
using System.Data;
using System.Data.SqlClient;
using System.Linq;
using System.Windows.Forms;

namespace GroupByColumnsApp
{
    public partial class MainForm : Form
    {
        private const string connectionString = ""; // Veritabanı bağlantı dizesini ayarlayın

        public MainForm()
        {
            InitializeComponent();
        }

        private void MainForm_Load(object sender, EventArgs e)
        {
            LoadData();
        }

        private void LoadData()
        {
            using (SqlConnection connection = new SqlConnection(connectionString))
            {
                try
                {
                    connection.Open();

                    // Tüm kolonları çeken sorgu
                    string sqlQuery = "SELECT * FROM YourTable";
                    SqlDataAdapter adapter = new SqlDataAdapter(sqlQuery, connection);

                    // Veri tablosunu doldur
                    DataTable dataTable = new DataTable();
                    adapter.Fill(dataTable);

                    // Kolonları grupla ve DataGridView'e ekle
                    var groupedData = GroupByColumns(dataTable);
                    dataGridView1.DataSource = groupedData;

                }
                catch (Exception ex)
                {
                    MessageBox.Show($"Hata: {ex.Message}");
                }
            }
        }

        private DataTable GroupByColumns(DataTable originalTable)
        {
            // Tüm kolonlardaki değerleri birleştirip gruplamak için bir sütun ekleyin
            originalTable.Columns.Add("GroupByColumn", typeof(string));

            foreach (DataRow row in originalTable.Rows)
            {
                string concatenatedValues = "";
                foreach (DataColumn column in originalTable.Columns)
                {
                    concatenatedValues += row[column].ToString();
                }
                row["GroupByColumn"] = concatenatedValues;
            }

            // Yeni bir DataTable oluşturun ve gruplanmış verileri ekleyin
            DataTable groupedTable = new DataTable();
            groupedTable.Columns.Add("GroupByColumn", typeof(string));
            groupedTable.Columns.Add("Count", typeof(int));

            var groupedRows = originalTable.AsEnumerable()
                .GroupBy(r => r.Field<string>("GroupByColumn"))
                .Select(g => new
                {
                    GroupByColumn = g.Key,
                    Count = g.Count()
                });

            foreach (var group in groupedRows)
            {
                groupedTable.Rows.Add(group.GroupByColumn, group.Count);
            }

            return groupedTable;
        }
    }
}



using System;
using System.Data.SqlClient;

class Program
{
    static void Main()
    {
        // Veritabanı bağlantı dizesini belirtin
        string connectionString = "";

        // SQL sorgusu
        string sqlQuery = "SELECT COUNT(Column1) AS Column1Count FROM YourTable";

        // SqlConnection oluştur
        using (SqlConnection connection = new SqlConnection(connectionString))
        {
            // SqlCommand oluştur
            using (SqlCommand command = new SqlCommand(sqlQuery, connection))
            {
                try
                {
                    // Bağlantıyı aç
                    connection.Open();

                    // Sorguyu çalıştır ve sonucu al
                    int count = (int)command.ExecuteScalar();

                    // Sonucu ekrana yazdır
                    Console.WriteLine($"Column1'deki değerlerin sayısı: {count}");
                }
                catch (Exception ex)
                {
                    Console.WriteLine($"Hata: {ex.Message}");
                }
            }
        }
    }
}

