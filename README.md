# ImageJ-Macros
Macros written to automate image processing tasks

You have duochannel images and wish to save each channel as separate image files? Here I have two, magenta and blue, and save them separately with the prefix "tracer-" for magenta and "DAPI-" for blue.

function action(input, output, filename) {
        open(input + filename);
        run("Blue", "position=2");
		run("Magenta", "position=1");
		filename = getTitle();
		run("Split Channels");
		selectWindow("C1-" + filename);
		saveAs("PNG", output + "tracer" + "-" + filename);
		close();
		selectWindow("C2-" + filename);
		saveAs("PNG", output + "DAPI" + "-" + filename);
        close();
}

input = getDirectory("Choose input folder");
output = getDirectory("Choose output folder");

setBatchMode(true); 
list = getFileList(input);
for (i = 0; i < list.length; i++)
        action(input, output, list[i]);
setBatchMode(false);
