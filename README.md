# Notepad
Программа набора текста в формате RTF
// Code

using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace Notepad
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        OpenFileDialog ofd = new OpenFileDialog();
        SaveFileDialog sfd = new SaveFileDialog();
        PrintDialog print = new PrintDialog();
        ColorDialog cd = new ColorDialog();
        FontDialog fd = new FontDialog();
        dlgAboutBox dlgAbout = new dlgAboutBox();
        PrintPreviewDialog PrintPreview = new PrintPreviewDialog();



        private void Form1_Load(object sender, EventArgs e)
        {
            отменадействияToolStripMenuItem.Enabled = false;
            отменадействияToolStripMenuItem.Visible = false;

            this.Text = "Блокнот";
            toolStripStatusLabel1.Text = "Готов, Начните вводить Текст...";
            richTextBox1.Multiline = true;
            richTextBox1.ContextMenuStrip = contextMenuStrip1;
        }

        private void СохранитьToolStripMenuItem_Click(object sender, EventArgs e)
        {
            sfd.Filter = "RTF Формат (*.rtf)|*.rtf|All files (*.*)|*.*";
            sfd.ShowDialog();

            richTextBox1.SaveFile(sfd.FileName, RichTextBoxStreamType.RichText);
        }

        private void СохранитькакToolStripMenuItem_Click(object sender, EventArgs e)
        {
            sfd.Filter = "RTF Формат (*.rtf)|*.rtf|All files (*.*)|*.*";
            sfd.ShowDialog();

            richTextBox1.SaveFile(sfd.FileName, RichTextBoxStreamType.RichText);
        }

        private void ВыходToolStripMenuItem_Click(object sender, EventArgs e)
        {
            if(richTextBox1.Text.Length == 0)
            {
                Application.Exit();
            }
            else
            {
                sfd.Filter = "RTF Формат (*.rtf)|*.rtf|All files (*.*)|*.*";
                sfd.ShowDialog();
                richTextBox1.SaveFile(sfd.FileName, RichTextBoxStreamType.RichText);

            }
        }

        private void ВырезатьToolStripMenuItem_Click(object sender, EventArgs e)
        {
            richTextBox1.Cut();
        }

        private void КопироватьToolStripMenuItem_Click(object sender, EventArgs e)
        {
            richTextBox1.Copy();
        }

        private void ВставкаToolStripMenuItem_Click(object sender, EventArgs e)
        {
            richTextBox1.Paste();
        }

        private void ВыделитьвсеToolStripMenuItem_Click(object sender, EventArgs e)
        {
            richTextBox1.SelectAll();
        }

        private void ОтменадействияToolStripMenuItem1_Click(object sender, EventArgs e)
        {
            richTextBox1.Undo();
        }

        private void ОпрограммеToolStripMenuItem_Click(object sender, EventArgs e)
        {
            dlgAbout.ShowDialog();
        }

        private void ПредварительныйпросмотрToolStripMenuItem_Click(object sender, EventArgs e)
        {
            PrintPreview.ShowDialog();
        }

        private void ПечатьToolStripMenuItem_Click(object sender, EventArgs e)
        {
            print.ShowDialog();
        }

        private void ШрифтToolStripMenuItem_Click(object sender, EventArgs e)
        {
            fd.ShowDialog();
            richTextBox1.Font = fd.Font;
        }

        private void ЦветToolStripMenuItem_Click(object sender, EventArgs e)
        {
            cd.ShowDialog();
            richTextBox1.SelectionColor = cd.Color;
        }

        private void ПоискToolStripMenuItem1_Click(object sender, EventArgs e)
        {
            FindText(richTextBox1.Text);
        }

        public bool FindText(string text)
        {
            // Initialize the return value to false by default. 
            bool returnValue = false;

            // Ensure a search string has been specified. 
            if (text.Length > 0)
            {
                // Obtain the location of the search string in richTextBox1. 
                int indexToText = richTextBox1.Find(text, RichTextBoxFinds.MatchCase);
                // Determine if the text was found in richTextBox1. 
                if (indexToText >= 0)
                {
                    returnValue = true;
                }
            }

            return returnValue;
        }
    }
}
