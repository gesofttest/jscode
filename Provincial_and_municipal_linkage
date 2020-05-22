/**
 * 省市联动封装
 * 
 * 调用方法：$(document).chinaReact.get(opt);
 * data.json为省市区数据
 * var opt = {
	chinaDom: '0',
	pdom: 'search_Province',
	cdom: 'search_City',
	ddom: 'search_District',
	url: '/data.json',
}
 */
(function($) {
	$.fn.extend({
		chinaReact : {
			get : function(opt, callback) {
				getProvince(opt.url, opt);
				$(document).on('change', opt.pdom, function() {
					// console.log($('#' + opt.pdom).find("option:selected").attr("data-no"));
					var province_data = $(opt.pdom).find("option:selected").attr("data-no");
					if (getNullValue($(opt.pdom).val()) != '') {
						$.getJSON(opt.url, function(res) {
							var html = '';
							html += '<option value="">--所在市--</option>';
							//data
							//							$.each(res[province_data], function(i, n) {
							//								html += '<option value=\'' + n + '\' data-no="' + i + '">' + n + '</option>';
							//							})
							//data2
							$.each(res[opt.chinaDom + ',' + province_data], function(i, n) {
								html += '<option value=\'' + n + '\' data-no="' + opt.chinaDom + ',' + province_data + ',' + i + '">' + n + '</option>';
							})
							$(opt.cdom).html(html);
							$(opt.ddom).html('<option value="">--所在区--</option>');
						})
					} else {
						$(opt.cdom).html('<option value="">--所在市--</option>');
						$(opt.ddom).html('<option value="">--所在区--</option>');
					}
				})
				$(document).on('change', opt.cdom, function() {
					var city_data = $(opt.cdom).find("option:selected").attr("data-no");
					if (getNullValue($(opt.cdom).val()) != '') {
						$.getJSON(opt.url, function(res) {
							var html = '';
							html += '<option value="">--所在区--</option>';
							$.each(res[city_data], function(i, n) {
								html += '<option value=\'' + n + '\' data-no="' + i + '">' + n + '</option>';
							})
							$(opt.ddom).html(html);
						})
					} else {
						$(opt.ddom).html('<option value="">--所在区--</option>');
					}
				})
			},
			clean : function(opt, callback) {
				$(opt.pdom).val('');
				$(opt.cdom).html('<option value="">--所在市--</option>');
				$(opt.ddom).html('<option value="">--所在区--</option>');
				if (callback)
					callback();
			},
			set : function(opt) {
				if (opt.p == null || typeof (opt.p) == "undefined" || opt.p == '') {
					return this.clean(opt);
				}
				$.getJSON(opt.url, function(res) {
					var html = '';
					var pnum = null;
					var cnum = null;
					var dnum = null;
					html += '<option value="">--所在省--</option>';
					$.each(res[opt.chinaDom], function(i, n) {
						var selected = '';
						if (opt.p == n) {
							selected = 'selected';
							pnum = i;
						}
						html += '<option ' + selected + ' value=\'' + n + '\' data-no="' + i + '">' + n + '</option>';
					})
					$(opt.pdom).html(html);
					opt.pnum = pnum;
					var html1 = '';
					html1 += '<option value="">--所在市--</option>';
					$.each(res[opt.chinaDom + ',' + pnum], function(i, n) {
						var selected = '';
						if (opt.c == n) {
							selected = 'selected';
							cnum = i;
						}
						html1 += '<option ' + selected + ' value=\'' + n + '\' data-no="' + opt.chinaDom + ',' + pnum + ',' + i + '">' + n + '</option>';
					})
					$(opt.cdom).html(html1);
					opt.cnum = cnum;
					if (opt.c == null || typeof (opt.c) == "undefined" || opt.c == '') {
						return;
					}
					var html2 = '';
					html2 += '<option value="">--所在区--</option>';
					$.each(res[opt.chinaDom + ',' + pnum + ',' + cnum], function(i, n) {
						var selected = '';
						if (opt.d == n) {
							selected = 'selected';
							dnum = i;
						}
						html2 += '<option ' + selected + ' value=\'' + n + '\' data-no="' + i + '">' + n + '</option>';
					})
					$(opt.ddom).html(html2);
					opt.dnum = dnum;
				});
			},
			setCall : function(opt, callback) {
				this.set(opt);
				if (callback) {
					callback();
				}
			}
		},
	})
  //此处为ckeditor
	$.extend({
		getProductIndustry : function(param, callback) {
			$.get(param.url, function(res) {
				callback(res);
			})
		},
		createEdit : function(edit, callback) {
			var ckeditor;
			ckeditor = CKEDITOR.replace(edit.ckEditorDom, {
				filebrowserUploadUrl : '/ckeditorupload/upload.action?TYPE=File',
				filebrowserImageUploadUrl : '/ckeditorupload/upload.action?TYPE=Image&',
				filebrowserFlashUploadUrl : '/ckeditorupload/upload.action?TYPE=Flash',
				height : '500px'
			});
			edit.ckeditor = ckeditor;
			if (callback)
				callback();
		}
	})
	function getProvince(url, opt) {
		$.getJSON(opt.url, function(res) {
			var html = '';
			html += '<option value="">--所在省--</option>';
			$.each(res[opt.chinaDom], function(i, n) {
				html += '<option value=\'' + n + '\' data-no="' + i + '">' + n + '</option>';
			})
			$(opt.pdom).html(html);
			$(opt.cdom).html('<option value="">--所在市--</option>');
			$(opt.ddom).html('<option value="">--所在区--</option>');
		})
	}
})(jQuery);
