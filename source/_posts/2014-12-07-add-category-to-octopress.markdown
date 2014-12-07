---
layout: post
title: "add category to octopress"
date: 2014-12-07 23:05:39 +0800
comments: true
categories: octopress
---

#####1. 新建插件文件plugins/category_list_tag.rb, 内容如下:  
    module Jekyll  
      class CategoryListTag < Liquid::Tag  
        def render(context)  
          html = ""  
          categories = context.registers[:site].categories.keys  
          categories.sort.each do |category|  
            posts_in_category = context.registers[:site].categories[category].size  
            category_dir = context.registers[:site].config['category_dir']  
            category_url = File.join(category_dir, category.gsub(/_|\P{Word}/, '-').gsub(/-{2,}/, '-').downcase)  
            html << "<li class='category'><a href='/#{category_url}/'>#{category} (#{posts_in_category})</a></li>\n"  
          end  
          html  
        end  
      end  
    end  
    
    Liquid::Template.register_tag('category_list', Jekyll::CategoryListTag)  

#####2. 新建source/_includes/asides/category_list.html文件，内容如下：  
    <section>  
      <h1>Categories</h1>  
      <ul id="categories">  
        { % category_list % }  
      </ul>  
    </section>  

#####3. 修改_config.yml文件，在default_asides项中添加asides/category_list.html, 值之间以逗号隔开:  
    default_asides:[asides/category_list.html, asides/recent_posts.html, ...]  

#####4. rake generate; rake preview; rake deploy;  


- - -
#####参考资料：
[http://www.cnblogs.com/oec2003/archive/2013/05/31/3109577.html](http://www.cnblogs.com/oec2003/archive/2013/05/31/3109577.html)  

