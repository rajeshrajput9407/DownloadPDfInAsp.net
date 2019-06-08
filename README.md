# DownloadPDfInAsp.net
Download PDf In Asp.net using Itextsharp

using (System.IO.MemoryStream memoryStream = new System.IO.MemoryStream())
            {
                string pdfTemplate = @"D:\VSB5E.pdf";

                PdfReader pdfReader = new PdfReader(pdfTemplate);
                PdfStamper pdfStamper = new PdfStamper(pdfReader, memoryStream);
                AcroFields pdfFormFields = pdfStamper.AcroFields;
                // set form pdfFormFields  
                // The first worksheet and W-4 form  
                //pdfFormFields.SetField("f1_01(0)", "1");

                pdfFormFields.SetField("CustFullName", "Rajesh");
                // report by reading values from completed PDF  
                // flatten the form to remove editting options, set it to false  
                // to leave the form open to subsequent manual edits  
                pdfStamper.FormFlattening = false;
                // close the pdf  
                pdfStamper.Close();

                byte[] bytes = memoryStream.ToArray();
                memoryStream.Close();
                Response.Clear();
                Response.ContentType = "application/pdf";
                Response.AddHeader("Content-Disposition", "attachment; filename=Employee.pdf");
                Response.ContentType = "application/pdf";
                Response.Buffer = true;
                Response.Cache.SetCacheability(HttpCacheability.NoCache);
                Response.BinaryWrite(bytes);
                Response.End();
                Response.Close();
