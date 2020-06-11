# Notes for Week 6

This week I am using the Mrs. Thompson Advises column in the Globe and Mail from 1950-1959 that returns the search word alcohol to examine the societal impacts of alcohol on family life.

First, I downloaded all the articles and OCR'd them in R to get txt files.
              
              # tell R which packages you need
             library(magick)             
             library(magrittr)                 
                 library(tesseract)                 
                 imgsource <- "many-pics"                 
                 myfiles <- list.files(path = imgsource, pattern = "png", full.names = TRUE)                   
                   lapply(myfiles, function(i){                   
                   text <- image_read(i) %>%                  
                  image_resize("3000x") %>%                   
                   image_convert(type = 'Grayscale') %>%                   
                   image_trim(fuzz = 40) %>%                   
                   image_write(format = 'png', density = '300x300') %>%
                   tesseract::ocr()                   
                   outfile <- paste(i,"-ocr.txt",sep="")
                   cat(text, file=outfile, sep="\n")
                  })

Then I ran them through the Topic Modelling Tool.

