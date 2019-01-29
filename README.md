# ImageJ-Macros
Macros written to automate image processing tasks
You have a bunch of multichannel images but the contrast on channel two is weak so you want to enhance it to make crisp images for your presentation slides? Saturation level 80% works well but try it out for yourself. Note: This macro works on image batches and saves the edited images in a whichever folder you want with the same file name. If you pick the same folder for output the images will just be replaced.

function action(input, output, filename) {
	 open(input + filename);
	 filename = getTitle();
	 setSlice(2);
	 run("Enhance Contrast", "saturated=0.80");
	 save(output + filename);
	 close();
}

input = getDirectory("Choose input folder");
output = getDirectory("Choose output folder");

setBatchMode(true); 
list = getFileList(input);
for (i = 0; i < list.length; i++)
        action(input, output, list[i]);
setBatchMode(false);
