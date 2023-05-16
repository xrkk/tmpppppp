pypdf2 error example pdf: https://github.com/py-pdf/pypdf/issues/1832



In [1]: import PyPDF2                                                                                                                               
                                                                                                                                                    
In [2]: f_pdf = '/mnt/f/pdf-note/2021 ---- book - Security of biquitous Computing Systems.pdf'                                                      
                                                                                                                                                    
In [3]: pdf_reader = PyPDF2.PdfReader(f_pdf)                                                                                                        
                                                                                                                                                    
In [4]: pdf_reader.outline                                                                                                                          
---------------------------------------------------------------------------                                                                         
ValueError                                Traceback (most recent call last)                                                                         
Cell In[4], line 1                                                                                                                                  
----> 1 pdf_reader.outline                                                                                                                          
                                                                                                                                                    
File ~/anaconda3/envs/py3/lib/python3.10/site-packages/PyPDF2/_reader.py:745, in PdfReader.outline(self)                                            
    737 @property                                                                                                                                   
    738 def outline(self) -> OutlineType:                                                                                                           
    739     """                                                                                                                                     
    740     Read-only property for the outline (i.e., a collection of 'outline items'                                                               
    741     which are also known as 'bookmarks') present in the document.                                                                           
    742                                                                                                                                             
    743     :return: a nested list of :class:`Destinations<PyPDF2.generic.Destination>`.                                                            
    744     """                                                                                                                                     
--> 745     return self._get_outline()                                                                                                              
                                                                                                                                                    
File ~/anaconda3/envs/py3/lib/python3.10/site-packages/PyPDF2/_reader.py:774, in PdfReader._get_outline(self, node, outline)                        
    772         if lines is not None and "/First" in lines:                                                                                         
    773             node = cast(DictionaryObject, lines["/First"])                                                                                  
--> 774     self._namedDests = self._get_named_destinations()                                                                                       
    776 if node is None:                                                                                                                            
    777     return outline                                                                                                                          
                                                                                                                                                    
File ~/anaconda3/envs/py3/lib/python3.10/site-packages/PyPDF2/_reader.py:711, in PdfReader._get_named_destinations(self, tree, retval)              
    709 if isinstance(value, DictionaryObject) and "/D" in value:                                                                                   
    710     value = value["/D"]                                                                                                                     
--> 711 dest = self._build_destination(key, value)  # type: ignore                                                                                  
    712 if dest is not None:                                                                                                                        
    713     retval[key] = dest                                                                                                                      
                                                                                                                                                    
File ~/anaconda3/envs/py3/lib/python3.10/site-packages/PyPDF2/_reader.py:906, in PdfReader._build_destination(self, title, array)                   
    904 array = array[2:]                                                                                                                           
    905 try:                                                                                                                                        
--> 906     return Destination(title, page, Fit(fit_type=typ, fit_args=array))  # type: ignore                                                      
    907 except PdfReadError:                                                                                                                        
    908     logger_warning(f"Unknown destination: {title} {array}", __name__)                                                                       
                                                                                                                                                    
File ~/anaconda3/envs/py3/lib/python3.10/site-packages/PyPDF2/generic/_data_structures.py:1256, in Destination.__init__(self, title, page, fit)     
   1254 # from table 8.2 of the PDF 1.7 reference.                                                                                                  
   1255 if typ == "/XYZ":                                                                                                                           
-> 1256     (                                                                                                                                       
   1257         self[NameObject(TA.LEFT)],                                                                                                          
   1258         self[NameObject(TA.TOP)],                                                                                                           
   1259         self[NameObject("/Zoom")],                                                                                                          
   1260     ) = args                                                                                                                                
   1261 elif typ == TF.FIT_R:                                                                                                                       
   1262     (                                                                                                                                       
   1263         self[NameObject(TA.LEFT)],                                                                                                          
   1264         self[NameObject(TA.BOTTOM)],                                                                                                        
   1265         self[NameObject(TA.RIGHT)],                                                                                                         
   1266         self[NameObject(TA.TOP)],                                                                                                           
   1267     ) = args                                                                                                                                
                                                                                                                                                    
ValueError: not enough values to unpack (expected 3, got 2)                                                                                         
