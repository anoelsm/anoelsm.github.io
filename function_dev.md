---
layout: page
title: Unofficially developing functions
image: 
---

<h2>Preamble</h2>

<p>While I do admit that this mostly stems from stubborness, I have two philosophies with programming (at least in R): 1) if I have to repeat it then it should be a function; and 2) there has to be a way to create the data visualizations I am imagining without saving things and moving into Illustrator. Yes I know it's easier to copy and paste, yes I know it's easier to just save it and edit small things in post later, but again, I'm stubborn. So here are things I've done that I want to save and maybe use in the future that I developed but weren't actually utilized.</p>

<hr class="major" />

<dl class="accordion">
  <dt>Have you ever wanted to include both color and patterns in a nested bar chart? Problably not but here ya go...</dt>
  <dd><h3>Okay this is a very specific example.</h3>
  <p>Problem: The problem is that I want to use a specific package common in microbial ecology to created nested bar graphs. This is because I want the colorbar which allows for different species to be colored as shades of colors assigned to higher taxonomic groups. For example, diatoms here are colored as shades of green. This allows for easy visualization of species and microbial groups within each stacked bar graph. However, in this example there are a lot of diatom species so it's hard to distinguish between them when you look from one group to the next. I had an idea to input patterns on the areas for specific species I want to highlight. It's simple to create patterns bar charts when you're just using basic ggplot2, but here I wanted to use this specific function <i>ggnested</i>.</p>
  <p>Solution: I appended the <i>ggnested</i> function to create <i>ggnested_pattern</i> which takes in a vector of patterns in the <i>aesthetics</i> and a) manually assigns patterns to species, and b) manually edits the legend to add the unique pattern onto each species.</p>
    <p> The following code creates this graph:
  <pre><code>library(ggplot2)
  library(ggnested)
  source(ggnested_pattern.R)
  df %>%
  mutate(
        phytogroups = factor(phytogroups,
                              levels = c("Diatoms", "Dinoflagellates",
                                        "MAST", "Greenalgae",
                                        "Haptophytes", "Rhodophytes",
                                        "Cryptophytes"), 
                              labels = c("Diatoms", "Dinoflagellates",
                                         "MAST", "Green algae",
                                         "Haptophytes", "Rhodophytes",
                                         "Cryptophytes")),
         pat = case_when(phytogroups == "Diatoms" & groups == "2"~"wave",
                         phytogroups == "Diatoms" & groups == "3"~"stripe",
                         TRUE~"none"),
         pat = if_else(Species == "Porosira_sp.", "circle", pat)) %>%
  ggnested_pattern(data = ., aes_string(main_group = "phytogroups",
                                sub_group = "Species", 
                                x = "groups", y = "sp_rel", pattern = "pat"),
           main_palette = group_colors) + 
  geom_col_pattern(pattern_fill="white", pattern_color="white", pattern_key_scale_factor=0.25,
                   pattern_size = 0.1) +
  scale_y_continuous(name = "Relative abundance",
                     expand = c(0,0)) +
  scale_x_continuous(name = "Cluster", expand = c(1E-3,1E-3), breaks = c(1,2,3)) +
  theme_nested(theme_linedraw) + 
  theme(
    axis.text = element_text(color = "black", size = 11),
    axis.title = element_text(size = 12),
    legend.title = element_blank(),
    panel.border = element_rect(color = "black")) +
  guides(fill=guide_legend(ncol = 1))
</code></pre>
</p>
  </dd>
</dl>

