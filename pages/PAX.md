- file format:
	- page_header [column_mini_page]+
	- page_header := pid   [start_offset]+ attributes_num records_num attribute_size free_space
	- column_mini_page := values [presence_bits|v-offsets]
- pros
	- 同一列存放在一起，提升了cache locality；方便压缩
	- 同一个表中的所有列值存放在一起
	- 不会增加disk IO
	-
-