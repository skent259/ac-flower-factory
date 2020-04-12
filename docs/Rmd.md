# R Markdown

## Adding appendix to file


    ## Appendix: R Code

    ```{r appendix, ref.label=knitr::all_labels(),echo=TRUE,eval=FALSE}
    ```

## Options 

#### Reasonable for reports

    ```{r setup, include=FALSE}
    knitr::opts_chunk$set(echo = FALSE, cache = TRUE, warning = FALSE, message = FALSE)
    knitr::opts_chunk$set(fig.width=10, fig.height=5) 
    ```

## Tables

A reasonable default table (requires `knitr` and `kableExtra`)

    ```{r}
    kable_standard <- function(...) {
    kable(booktabs = TRUE, ...) %>% 
        kable_styling(full_width = FALSE)
    }
    ```

Note that adding `latex_options = c("hold_position)` may be useful in holding tables to their current position.  I wasn't able to get it to work.  An alternative (but tedious) option is to add `keep_tex: TRUE` to the YAML (under `pdf_document:`) and manually add [!htbp] at the end of the `\begin{figure}` line in the .tex file.  

Almost anything you'd want to do with a latex table can be found at [Create Awesome LaTeX Table with knitr::kable and kableExtra](https://haozhu233.github.io/kableExtra/awesome_table_in_pdf.pdf)
