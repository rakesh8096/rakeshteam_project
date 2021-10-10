# rakeshteam_project
//**PROGRAM.CS  **//
using System;
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace rakeshteam_project
{
    static class Program
    {
        /// <summary>
        /// The main entry point for the application.
        /// </summary>
        [STAThread]
        static void Main()
        {
            Application.EnableVisualStyles();
            Application.SetCompatibleTextRenderingDefault(false);
            Application.Run(new dashboard());
        }
    }
}


//**DASHBOARD.CS**//

using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace rakeshteam_project
{
    public partial class dashboard : Form
    {
        public dashboard()
        {
            InitializeComponent();
        }

        private void btnaddoffer_Click(object sender, EventArgs e)
        {
           // addoffers ob = new addoffers();
            addoffers ob = new addoffers();
            ob.Show();

        }

        private void btnaddcustomer_Click(object sender, EventArgs e)
        {
            addcustomer ob1 = new addcustomer();
            ob1.Show();

        }

        private void btnaddorders_Click(object sender, EventArgs e)
        {
            orders ob2 = new orders();
            ob2.Show();

        }

        private void btnaddcategories_Click(object sender, EventArgs e)
        {
            addcategories ob3 = new addcategories();
            ob3.Show();
        }
    }
}

//** FOR OFFERS **//

using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Text.RegularExpressions;
using System.Threading.Tasks;
using System.Windows.Forms;


namespace rakeshteam_project
{
    public partial class addoffers : Form
    {
        DataTable dt;
        DataColumn dc;
        DataRow dr;
        DataTable offers;
        public addoffers()
        {
            InitializeComponent();
        }

        private void txtofferid_TextChanged(object sender, EventArgs e)
        {
                if (Regex.IsMatch(txtofferid.Text, "[^0-9]"))

                {
                    MessageBox.Show("Do not enter non-numeric value" + txtofferid.Text);
                    txtofferid.Text = "";
                }
        }

        private void txtdiscount_TextChanged(object sender, EventArgs e)
        {
                if (Regex.IsMatch(txtdiscount.Text, "[^0-9]"))

                {
                    MessageBox.Show("Do not enter non-numeric value" + txtdiscount.Text);
                    txtdiscount.Text = "";
                }
        }

        private void txtpromosource_TextChanged(object sender, EventArgs e)
        {

        }

        private void btnsubmit_Click(object sender, EventArgs e)
        {
            string offerid, discount, promosource;
            offerid = txtofferid.Text;
            discount = txtdiscount.Text;
            promosource = txtpromosource.Text;
            try
            {
                dr = offers.NewRow();
                dr[0] = int.Parse(offerid);
                dr[1] = float.Parse(discount);
                dr[2] = promosource;
                offers.Rows.Add(dr);
            }
            catch (Exception ob)
            {
                MessageBox.Show(ob.Message);
            }

            clear();
        }
        private void clear()
        {
            txtofferid.Text = "";
            txtdiscount.Text = "";
            txtpromosource.Text = "";
        }


    

    private void addoffers_Load(object sender, EventArgs e)
    {
         offers = Generatetable();
        dataGridView1.DataSource = offers;


    }
    DataTable Generatetable()
    {
        dt = new DataTable("addoffers");

        dc = new DataColumn("OfferID", typeof(int));
        dt.Columns.Add(dc);
        dt.PrimaryKey = new DataColumn[] { dc };

        dc = new DataColumn("DISCOUNT", typeof(float));
        dt.Columns.Add(dc);

        dc = new DataColumn("PROMOCODE", typeof(String));
        dt.Columns.Add(dc);
        return dt;

    }

        private void dataGridView1_CellContentClick(object sender, DataGridViewCellEventArgs e)
        {

        }
    }
}

//**FOR CUSTOMER **//

using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Text.RegularExpressions;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace WindowsFormsApp3
{
    //ADD_Customer
    public partial class Form1 : Form
    {
        DataTable dt;
        DataColumn dc;
        DataRow dr;
        DataTable cust;
        public Form1()
        {
            InitializeComponent();
        }

        private void Form1_Load(object sender, EventArgs e)
        {
            cust = GetCustomerDetails();
            dataGridView1.DataSource = cust;
        }
        DataTable GetCustomerDetails()
        {
            dt = new DataTable("CUSTOMERS");

            dc = new DataColumn("CustomerID", typeof(int));
            dt.Columns.Add(dc);
            dt.PrimaryKey = new DataColumn[] { dc };

            dc = new DataColumn("CustomerName", typeof(string));
            dt.Columns.Add(dc);

            dc = new DataColumn("CustomerContact", typeof(int));
            dt.Columns.Add(dc);

            dc = new DataColumn("CustomerEmail", typeof(string));
            dt.Columns.Add(dc);

            dc = new DataColumn("CustomerAddress", typeof(string));
            dt.Columns.Add(dc);

            return dt;
        }

        private void label5_Click(object sender, EventArgs e)
        {

        }

        private void textBox1_TextChanged(object sender, EventArgs e)
        {
            if (Regex.IsMatch(txtcid.Text, "[^0-9]"))
            {
                MessageBox.Show("Do not enter non numeric  value.");
                txtcid.Text = "";
            }
        }
        private void btnSubmit_Click(object sender, EventArgs e)
        {
            string cid, cname, ccont, cemail, cadd;
            cid = txtcid.Text;
            cname = txtcname.Text;
            ccont = txtcontact.Text;
            cemail = txtemail.Text;
            cadd = txtaddress.Text;

            try
            {
                dr = cust.NewRow();

                dr[0] = int.Parse(cid);
                dr[1] = cname;
                dr[2] = int.Parse(ccont);
                dr[3] = cemail;
                dr[4] = cadd;
                cust.Rows.Add(dr);
            }
            catch(Exception ob)
            {
                MessageBox.Show(ob.Message);
            }
            clear();
        }
        private void clear()
        {
            txtcid.Text="";
            txtcname.Text="";
            txtcontact.Text="";
            txtemail.Text="";
            txtaddress.Text="";
        }

        private void txtcontact_TextChanged(object sender, EventArgs e)
        {
            if (Regex.IsMatch(txtcontact.Text, "[^0-9]"))
            {
                MessageBox.Show("Do not enter non numeric  value.");
                txtcontact.Text = "";
            }
        }
    }
}

//** FOR CATOGIRIES **//

public partial class Categories : Form
    {
        DataTable dt;
        DataColumn dc;
        DataRow dr;
        DataTable Cat;
        public Categories()
        {
            InitializeComponent();
        }

        private void label1_Click(object sender, EventArgs e)
        {

        }

        private void Categories_Load(object sender, EventArgs e)
        {
            Cat = Generatetable();
            dataGridView1.DataSource = Cat;
        }
        DataTable Generatetable()
        {
            dt = new DataTable("Categories");
            dc = new DataColumn("CatId", typeof(int));
            dt.Columns.Add(dc);
            dt.PrimaryKey = new DataColumn[] { dc };
            dc = new DataColumn("CatName", typeof(string));
            dt.Columns.Add(dc);
            dc = new DataColumn("CatDesc", typeof(string));
            dt.Columns.Add(dc);
            return dt;
        }

        private void button1_Click(object sender, EventArgs e)
        {
            String catid, catname, catdesc;
            catid = txtcatid.Text;
            catname = txtcatname.Text;
            catdesc = txtcatdesc.Text;
            try
            {
                dr = Cat.NewRow();
                dr[0] = int.Parse(catid);
                dr[1] = catname;
                dr[2] = catdesc;
                Cat.Rows.Add(dr);
            }
            catch (Exception ob)
            {
                MessageBox.Show(ob.Message);
            }
            clear();
        }
        private void clear()
        {
            txtcatid.Text = "";
            txtcatname.Text = "";
            txtcatdesc.Text = "";
        }

        private void txtcatid_TextChanged(object sender, EventArgs e)
        {
            if (Regex.IsMatch(txtcatid.Text, "[^0-9]"))
            {
                MessageBox.Show("Do not enter non numeric  value.");
                txtcatid.Text = "";
            }
        }
    }
    
    //** FOR ORDERS**//
    using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Text.RegularExpressions;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace PROJECT1
{
    public partial class Form1 : Form
    {
        DataTable dt;
        DataColumn dc;
        DataRow dr;
        DataTable orders;
        public Form1()
        {
            InitializeComponent();
        }

        private void Form1_Load(object sender, EventArgs e)
        {
             orders = Generatetable();
            dataGridView1.DataSource = orders;

        }
        DataTable Generatetable()
        {
            dt = new DataTable("ADDORDERS");

            dc = new DataColumn("ORDERID", typeof(int));
            dt.Columns.Add(dc);
            dt.PrimaryKey = new DataColumn[] { dc };

            dc = new DataColumn("PRODUCTID", typeof(int));
            dt.Columns.Add(dc);

            dc = new DataColumn("PRODUCTQUANTITY", typeof(int));
            dt.Columns.Add(dc);
            return dt;

        }
        private void lbpq_Click(object sender, EventArgs e)
        {

        }

        private void txtoid_TextChanged(object sender, EventArgs e)
        {
            {
                if (Regex.IsMatch(txtoid.Text, "[^0-9]"))

                {
                    MessageBox.Show("Do not enter non-numeric value" + txtoid.Text);
                    txtoid.Text = "";
                }
            }
        }

        private void btnsubmit_Click(object sender, EventArgs e)
        {
            string orderid, productid, pquantity;
            orderid = txtoid.Text;
            productid = txtpid.Text;
            pquantity = txtpq.Text;
            try {
                dr = orders.NewRow();
                dr[0] = int.Parse(orderid);
                dr[1] = int.Parse(productid);
                dr[2] = int.Parse(pquantity);
                orders.Rows.Add(dr);
            }
            catch(Exception ob)
            {
                MessageBox.Show(ob.Message);
            }

            clear();
        }
        private void clear()
        {
            txtoid.Text = "";
            txtpid.Text = "";
            txtpq.Text = "";
        }

      //  private void txtpid_ValueChanged(object sender, EventArgs e)
        
        private void txtpid_TextChanged(object sender, EventArgs e)
        {
            {
                if (Regex.IsMatch(txtpid.Text, "[^0-9]"))

                {
                    MessageBox.Show("Do not enter non-numeric value" + txtpid.Text);
                    txtpid.Text = "";
                }
            }

        }

        private void txtpq_TextChanged(object sender, EventArgs e)
        {
            {
                if (Regex.IsMatch(txtpq.Text, "[^0-9]"))

                {
                    MessageBox.Show("Do not enter non-numeric value" + txtpq.Text);
                    txtpq.Text = "";
                }
            }
        }
    }
}
