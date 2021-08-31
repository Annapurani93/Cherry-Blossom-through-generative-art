library(flametree)
library(jasmines)
library(dplyr)
library(magrittr)
library(ggplot2)
library(magick)
library(png)
flametree_grow(
  seed = 286,
  time = 6,
  scale = c(0.6, 0.8, 0.9),
  angle = c(-10, 10, 20),
  split = 2,
  trees =8,
  seg_col = spark_linear(tree = 3, time = 3),
  seg_wid = spark_decay(time = 0.3, multiplier = 4, constant = 0.1),
  shift_x = spark_random(multiplier = 8),
  shift_y = spark_nothing()
)  %>% 
  flametree_plot(
    background = "black",
    palette = c("#654321", "#ffb7c5"),
    style = "wisp"
  )->c1

c1

ggsave("c1.png", c1, width = 10, height = 10, units = "cm")


c0 <- use_seed(100) %>% # Set the seed of R‘s random number generator, which is useful for creating simulations or random objects that can be reproduced.
  scene_discs(
    rings = 60, 
    points = 6000, 
    size = 21
  ) %>%
  mutate(ind = 1:n()) %>%
  unfold_warp(
    iterations = 10,
    scale = .5, 
    output = "layer" 
  ) %>%
  unfold_tempest(
    iterations = 5,
    scale = .01
  ) %>%
  style_ribbon(
    color = "#FFA500",
    colour = "#FFA500",
    alpha = c(1,1),
    background = "black"
  )

c0

ggsave("c0.png", c0, width = 10, height = 10, units = "cm")


Trees <- image_read('c1.png')
Petals <- image_read("c0.png")
image_scale(Petals, "80")->Petals
image_scale(Trees,"600")->Trees
image_equalize(Petals)->Petals
image_composite(Trees, Petals, offset = "+380+380")->cb
cb%>%image_annotate("@annapurani93", size = 12, color = "white", location = "+20+455")->cb
cb
image_write(cb, path = "final.png", format = "png", quality = 100)
