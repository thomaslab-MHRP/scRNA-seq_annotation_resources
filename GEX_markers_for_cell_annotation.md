 

### Overview

 

The annotation of single-cell RNA-Seq data involves procedures for
demultiplexing 10x data from a sequencing run, alignment to a genome,
and extracting read counts for cells per sample; performed using
Cellranger. Subsequent analyses are done using the R library ‘Seurat’.

Cellranger produces a feature barcode matrix per sample, which is read
into a Seurat object, and then processed for quality control, involving
filtering cells for mitochondrial gene content \<10%, excluding cells
identified as hash doublets & negatives (if the dataset is hashed), as
well as cells from donors (as identified through hashing) containing
less than 2000 cells.

The identification of cell subset populations (as visualized in clusters
of the Seurat object), is performed using a set of lineage marker genes,
as listed in the table below. As part of additional QC, cell clusters
identified as ‘red blood cells’ (expressing HBB) are also removed from
the object.

 

<center>
<div id="tycmjjowvf" style="padding-left:0px;padding-right:0px;padding-top:10px;padding-bottom:10px;overflow-x:auto;overflow-y:auto;width:auto;height:auto;">
<style>#tycmjjowvf table {
  font-family: system-ui, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol', 'Noto Color Emoji';
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

#tycmjjowvf thead, #tycmjjowvf tbody, #tycmjjowvf tfoot, #tycmjjowvf tr, #tycmjjowvf td, #tycmjjowvf th {
  border-style: none;
}

#tycmjjowvf p {
  margin: 0;
  padding: 0;
}

#tycmjjowvf .gt_table {
  display: table;
  border-collapse: collapse;
  line-height: normal;
  margin-left: auto;
  margin-right: auto;
  color: #333333;
  font-size: 16px;
  font-weight: normal;
  font-style: normal;
  background-color: #FFFFFF;
  width: auto;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #5F5F5F;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #5F5F5F;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
}

#tycmjjowvf .gt_caption {
  padding-top: 4px;
  padding-bottom: 4px;
}

#tycmjjowvf .gt_title {
  color: #333333;
  font-size: 125%;
  font-weight: initial;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-color: #FFFFFF;
  border-bottom-width: 0;
}

#tycmjjowvf .gt_subtitle {
  color: #333333;
  font-size: 85%;
  font-weight: initial;
  padding-top: 3px;
  padding-bottom: 5px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-color: #FFFFFF;
  border-top-width: 0;
}

#tycmjjowvf .gt_heading {
  background-color: #FFFFFF;
  text-align: center;
  border-bottom-color: #FFFFFF;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
}

#tycmjjowvf .gt_bottom_border {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #5F5F5F;
}

#tycmjjowvf .gt_col_headings {
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #5F5F5F;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #5F5F5F;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
}

#tycmjjowvf .gt_col_heading {
  color: #FFFFFF;
  background-color: #5F5F5F;
  font-size: 100%;
  font-weight: normal;
  text-transform: inherit;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: bottom;
  padding-top: 5px;
  padding-bottom: 6px;
  padding-left: 5px;
  padding-right: 5px;
  overflow-x: hidden;
}

#tycmjjowvf .gt_column_spanner_outer {
  color: #FFFFFF;
  background-color: #5F5F5F;
  font-size: 100%;
  font-weight: normal;
  text-transform: inherit;
  padding-top: 0;
  padding-bottom: 0;
  padding-left: 4px;
  padding-right: 4px;
}

#tycmjjowvf .gt_column_spanner_outer:first-child {
  padding-left: 0;
}

#tycmjjowvf .gt_column_spanner_outer:last-child {
  padding-right: 0;
}

#tycmjjowvf .gt_column_spanner {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #5F5F5F;
  vertical-align: bottom;
  padding-top: 5px;
  padding-bottom: 5px;
  overflow-x: hidden;
  display: inline-block;
  width: 100%;
}

#tycmjjowvf .gt_spanner_row {
  border-bottom-style: hidden;
}

#tycmjjowvf .gt_group_heading {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #5F5F5F;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #5F5F5F;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: middle;
  text-align: left;
}

#tycmjjowvf .gt_empty_group_heading {
  padding: 0.5px;
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #5F5F5F;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #5F5F5F;
  vertical-align: middle;
}

#tycmjjowvf .gt_from_md > :first-child {
  margin-top: 0;
}

#tycmjjowvf .gt_from_md > :last-child {
  margin-bottom: 0;
}

#tycmjjowvf .gt_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  margin: 10px;
  border-top-style: none;
  border-top-width: 1px;
  border-top-color: #D5D5D5;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D5D5D5;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D5D5D5;
  vertical-align: middle;
  overflow-x: hidden;
}

#tycmjjowvf .gt_stub {
  color: #333333;
  background-color: #D5D5D5;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-right-style: solid;
  border-right-width: 2px;
  border-right-color: #D5D5D5;
  padding-left: 5px;
  padding-right: 5px;
}

#tycmjjowvf .gt_stub_row_group {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-right-style: solid;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  padding-left: 5px;
  padding-right: 5px;
  vertical-align: top;
}

#tycmjjowvf .gt_row_group_first td {
  border-top-width: 2px;
}

#tycmjjowvf .gt_row_group_first th {
  border-top-width: 2px;
}

#tycmjjowvf .gt_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#tycmjjowvf .gt_first_summary_row {
  border-top-style: solid;
  border-top-color: #5F5F5F;
}

#tycmjjowvf .gt_first_summary_row.thick {
  border-top-width: 2px;
}

#tycmjjowvf .gt_last_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #5F5F5F;
}

#tycmjjowvf .gt_grand_summary_row {
  color: #333333;
  background-color: #D5D5D5;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#tycmjjowvf .gt_first_grand_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-style: double;
  border-top-width: 6px;
  border-top-color: #5F5F5F;
}

#tycmjjowvf .gt_last_grand_summary_row_top {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: double;
  border-bottom-width: 6px;
  border-bottom-color: #5F5F5F;
}

#tycmjjowvf .gt_striped {
  background-color: #F4F4F4;
}

#tycmjjowvf .gt_table_body {
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #5F5F5F;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #5F5F5F;
}

#tycmjjowvf .gt_footnotes {
  color: #333333;
  background-color: #FFFFFF;
  border-bottom-style: none;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
}

#tycmjjowvf .gt_footnote {
  margin: 0px;
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#tycmjjowvf .gt_sourcenotes {
  color: #333333;
  background-color: #FFFFFF;
  border-bottom-style: none;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
}

#tycmjjowvf .gt_sourcenote {
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#tycmjjowvf .gt_left {
  text-align: left;
}

#tycmjjowvf .gt_center {
  text-align: center;
}

#tycmjjowvf .gt_right {
  text-align: right;
  font-variant-numeric: tabular-nums;
}

#tycmjjowvf .gt_font_normal {
  font-weight: normal;
}

#tycmjjowvf .gt_font_bold {
  font-weight: bold;
}

#tycmjjowvf .gt_font_italic {
  font-style: italic;
}

#tycmjjowvf .gt_super {
  font-size: 65%;
}

#tycmjjowvf .gt_footnote_marks {
  font-size: 75%;
  vertical-align: 0.4em;
  position: initial;
}

#tycmjjowvf .gt_asterisk {
  font-size: 100%;
  vertical-align: 0;
}

#tycmjjowvf .gt_indent_1 {
  text-indent: 5px;
}

#tycmjjowvf .gt_indent_2 {
  text-indent: 10px;
}

#tycmjjowvf .gt_indent_3 {
  text-indent: 15px;
}

#tycmjjowvf .gt_indent_4 {
  text-indent: 20px;
}

#tycmjjowvf .gt_indent_5 {
  text-indent: 25px;
}

#tycmjjowvf .katex-display {
  display: inline-flex !important;
  margin-bottom: 0.75em !important;
}

#tycmjjowvf div.Reactable > div.rt-table > div.rt-thead > div.rt-tr.rt-tr-group-header > div.rt-th-group:after {
  height: 0px !important;
}
</style>
<table class="gt_table" data-quarto-disable-processing="false" data-quarto-bootstrap="false">
  <thead>
    <tr class="gt_col_headings">
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1" scope="col" id="Cell-type">Cell type</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1" scope="col" id="Positive-gene-markers">Positive gene markers</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1" scope="col" id="Negative-gene-markers">Negative gene markers</th>
    </tr>
  </thead>
  <tbody class="gt_table_body">
    <tr><td headers="Cell type" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">Naïve B</td>
<td headers="Positive gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">CD19, IGHD</td>
<td headers="Negative gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;"></td></tr>
    <tr><td headers="Cell type" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">Memory B</td>
<td headers="Positive gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">CD19, CD27, IGHG1, MS4A1</td>
<td headers="Negative gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;"></td></tr>
    <tr><td headers="Cell type" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">CD14+ monocytes</td>
<td headers="Positive gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">CD14, S100A8, CD4</td>
<td headers="Negative gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;"></td></tr>
    <tr><td headers="Cell type" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">CD16+ monocytes</td>
<td headers="Positive gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">FCGR3A, CD4</td>
<td headers="Negative gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;"></td></tr>
    <tr><td headers="Cell type" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">NK (CD56dim)</td>
<td headers="Positive gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">GZMA, GZMB, GNLY, NKG7, FCGR3A</td>
<td headers="Negative gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">CD8A (very low expression possible)</td></tr>
    <tr><td headers="Cell type" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">CD56bright NK</td>
<td headers="Positive gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">NCAM1</td>
<td headers="Negative gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">TRDC, GZMK, GATA3</td></tr>
    <tr><td headers="Cell type" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">CD4+ naïve T</td>
<td headers="Positive gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">CD3E, CD4, CCR7, IL7R, TCF7, PTPRC, CD27 (low expression)</td>
<td headers="Negative gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;"></td></tr>
    <tr><td headers="Cell type" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">CD4+ central memory T (Tcm)</td>
<td headers="Positive gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">CD3E, CD4, CD27, SELL, CCR7</td>
<td headers="Negative gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">PTPRC</td></tr>
    <tr><td headers="Cell type" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">CD4+ effector memory T (Tem)</td>
<td headers="Positive gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">CD3E, CD4</td>
<td headers="Negative gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">CD27, CCR7, PTPRC, SELL, TCF7</td></tr>
    <tr><td headers="Cell type" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">CD4+ tissue resident memory T (Trm)</td>
<td headers="Positive gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">CD3E, CD4, CD69, ITGAE</td>
<td headers="Negative gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;"></td></tr>
    <tr><td headers="Cell type" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">CD4+ stem cell like memory T (Tscm)</td>
<td headers="Positive gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">CD3E, CD4, CD27, SELL, PTRPC, IL2RB, FAS</td>
<td headers="Negative gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;"></td></tr>
    <tr><td headers="Cell type" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">CD8+ naïve T</td>
<td headers="Positive gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">CD3E, CD8A, CCR7, TCF7, PTPRC, CD27 (low expression)</td>
<td headers="Negative gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;"></td></tr>
    <tr><td headers="Cell type" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">CD8+ central memory T (Tcm)</td>
<td headers="Positive gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">CD3E, CD8A, CD27, SELL, CCR7</td>
<td headers="Negative gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">PTPRC</td></tr>
    <tr><td headers="Cell type" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">CD8+ effector memory T (Tem)</td>
<td headers="Positive gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">CD3E, CD8A</td>
<td headers="Negative gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">CD27, CCR7, PTPRC, SELL, TCF7</td></tr>
    <tr><td headers="Cell type" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">CD8+ tissue resident memory T (Trm)</td>
<td headers="Positive gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">CD3E, CD8A, CD69, ITGAE</td>
<td headers="Negative gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;"></td></tr>
    <tr><td headers="Cell type" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">CD8+ stem cell like memory T (Tscm)</td>
<td headers="Positive gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">CD3E, CD8A, CD27, SELL, PTPRC, IL2RB, FAS</td>
<td headers="Negative gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;"></td></tr>
    <tr><td headers="Cell type" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">Mucosal-associated invariant T (MAIT)</td>
<td headers="Positive gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">CD3E, TRAV1-2, IL7R, GZMK, CCR6</td>
<td headers="Negative gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;"></td></tr>
    <tr><td headers="Cell type" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">Vγ9Vδ2 T</td>
<td headers="Positive gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">CD3E, TRGV9, TRDV2, GZMA, CCL5, TRDC</td>
<td headers="Negative gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;"></td></tr>
    <tr><td headers="Cell type" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">gdT</td>
<td headers="Positive gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">CD3E, TRGC1/TRGC2, TRDC</td>
<td headers="Negative gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">TRGV9, TRDV2</td></tr>
    <tr><td headers="Cell type" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">Regulatory T (Treg)</td>
<td headers="Positive gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">CD3E, FOXP3, IL2RA</td>
<td headers="Negative gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;"></td></tr>
    <tr><td headers="Cell type" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">Proliferating T (T-prolif)</td>
<td headers="Positive gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">CD3E, MKI67</td>
<td headers="Negative gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;"></td></tr>
    <tr><td headers="Cell type" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">Myeloid dendritic cells (mDC)</td>
<td headers="Positive gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">CST3, CD1C, HLA-DRA, CD4</td>
<td headers="Negative gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;"></td></tr>
    <tr><td headers="Cell type" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">Plasmacytoid dendritic cells (pDC)</td>
<td headers="Positive gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">CST3, CLEC4C, CXCR3, IL3RA, GZMB, CD4</td>
<td headers="Negative gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;"></td></tr>
    <tr><td headers="Cell type" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">Plasmablasts</td>
<td headers="Positive gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">JCHAIN, CD27, MKI67, IGHD, IGHG1</td>
<td headers="Negative gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;"></td></tr>
    <tr><td headers="Cell type" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">Megakaryocytes/Platelets</td>
<td headers="Positive gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">PPBP, ITGA2B</td>
<td headers="Negative gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;"></td></tr>
    <tr><td headers="Cell type" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">Hematopoietic stem cells (HSC)</td>
<td headers="Positive gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">CD34</td>
<td headers="Negative gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;"></td></tr>
    <tr><td headers="Cell type" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">Red blood cells (RBC)</td>
<td headers="Positive gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;">HBB, HBA1, HBA2</td>
<td headers="Negative gene markers" class="gt_row gt_left" style="border-top-width: 1.5px; border-top-style: solid; border-top-color: black; border-bottom-width: 1.5px; border-bottom-style: solid; border-bottom-color: black; border-left-width: 1.5px; border-left-style: solid; border-left-color: black; border-right-width: 1.5px; border-right-style: solid; border-right-color: black;"></td></tr>
  </tbody>
  
  
</table>
</div>
</center>

------------------------------------------------------------------------
