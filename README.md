# Profile
Social Networking project
<?php
	
public function img()
{     
   if($this->request->is('ajax'))  //checks if request is from ajax
   {	 
	   //$this->layout = false;		
              
    if ($this->request->is('post'))    // saving image path to db....
    {
		if ($this->data['Image']) 
		{
		    
		 $image = $this->data['Image']['image'];
		  
		   
          $uploadFolder = "uploadImg";                      //upload image folder
          $uploadPath = WWW_ROOT . $uploadFolder;           //upload image folder path
          $imageName = $image['name'];                 // image name
          
          $full_image_path = $uploadPath . '/' . $imageName;     //full image path
         
			if (move_uploaded_file($image['tmp_name'], $full_image_path))   //save the path name using move_uploaded_file
			{
				$this->request->data['Image']['path'] = $imageName;     //save the pathname in db
				$this->Image->save($this->data);   
				/*
				if($this->Image->save($this->data))
				{
					echo "sucessssssss"; echo "<br>";
					
					$this->loadModel('Image');
				    $id = $this->Image->getLastInsertId();  //get the last inserted id
				    print_r($id);
				    $countval = $this->Image->findById($id);    //findById
				     	//echo "<pre>";
	                 	//print_r($countval);
	                 	//$$countval['Image']['path']; 
	               json_encode($countval);
	               exit;  
				}    
				else
				{
					echo "fail";
				}*/
				//$this->Session->setFlash('File saved successfully');  
				$this->set('imageName',$imageName);  
			} else 
				{
					$this->Session->setFlash('There was a problem uploading file. Please try again.');
				}
		  
	     }
		
	}
             
   } 
} 			 
		   	 
	
    
    
    public function show(){
	
	   	$this->loadModel('Image');
	   	$data = $this->Image->find('all');
	   	//echo "<pre>";
	   	//print_r($data);
	   	$countval = $this->Image->find('count');
	   	//echo $countval  ;
	   	foreach($data as $dat){
			//print_r($dat);
			if($dat['Image']['id']==$countval){
					echo "<img src='../uploadImg/".$dat['Image']['path']."'/>";
			}
		} 
	   
	   	//echo "<img src='../uploads/".$imageName."'/>";
	}
	
}
    
?>
