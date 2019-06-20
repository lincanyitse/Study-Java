# 第四十九天

## Excel 读写

### 读取Excel

+ 读取Excel返回二维列表

    ```Java
    import org.apache.poi.hssf.usermodel.HSSFCell;
    import org.apache.poi.hssf.usermodel.HSSFRow;
    import org.apache.poi.hssf.usermodel.HSSFSheet;
    import org.apache.poi.hssf.usermodel.HSSFWorkbook;

    import java.io.File;
    import java.io.FileInputStream;
    import java.util.*;

    public class ExcelRead {
        public static List<List> excelRead(String path) {
            List<List> list = new ArrayList<>();
            try {
                File excel = new File(path);
                FileInputStream fis;
                // 获取文件输入流
                fis = new FileInputStream(excel);
                // 生成 excel 文档对象
                HSSFWorkbook sheets = new HSSFWorkbook(fis);
                System.out.println("开始读取");
                for (int i = 0; i <= sheets.getActiveSheetIndex(); i++) {
                    // 得到每一个 sheet
                    HSSFSheet sheet = sheets.getSheetAt(i);
                    for (int j = 1; j < sheet.getLastRowNum(); j++) {
                        // 得到每一行
                        HSSFRow row = sheet.getRow(j);
                        List<Object> map = new ArrayList<>();
                        for (int k = 0; k < row.getLastCellNum(); k++) {
                            // 得到每一格
                            HSSFCell cell = row.getCell(k);
                            map.add(cell);
                        }
                        list.add(map);
                    }
                }
                System.out.println(list);
                // 关闭文件输入流
                fis.close();
            } catch (Exception ex) {
                ex.printStackTrace();
            }
            return list;
        }
    }
    ```

### 写入Excel

+ 把`List<Obejct>`的`toString()`写入Excel

    ```Java
    import org.apache.poi.hssf.usermodel.HSSFCell;
    import org.apache.poi.hssf.usermodel.HSSFRow;
    import org.apache.poi.hssf.usermodel.HSSFSheet;
    import org.apache.poi.hssf.usermodel.HSSFWorkbook;

    import java.io.File;
    import java.io.FileNotFoundException;
    import java.io.FileOutputStream;
    import java.io.IOException;
    import java.util.List;
    import java.util.regex.Matcher;
    import java.util.regex.Pattern;

    public class ExcelWrite {
        public static boolean excelWrite(String path, String[] head,List list,int[] width) {
            boolean flag = false;
            try {
                // 1.获取excel文件
                File file = new File(path);
                FileOutputStream fos;
                // 2.创建到该文件的输出流
                fos = new FileOutputStream(file);
                // 新建一个工作簿
                HSSFWorkbook book = new HSSFWorkbook();
                // 新建一个sheet
                HSSFSheet sheet = book.createSheet();
                // 新建第1行
                HSSFRow row = sheet.createRow(0);
                // 设置标题栏
                for (int i = 0; i < head.length; i++) {
                    // 新建第1行第i个单元格
                    HSSFCell cell = row.createCell(i);
                    cell.setCellValue(head[i]);
                    // 设置表格第i列宽度为
                    sheet.setColumnWidth(i, width[i]);
                }
                // 写入数据
                for (int i = 0; i < list.size(); i++) {
                    // 新建第n行
                    row = sheet.createRow(i + 1);
                    // 从对象的toString提取数据 toString格式：类名[字段名1=数值1,字段名2=数值2,...]
                    String s = list.get(i).toString();
                    // 使用正则表达式
                    String regular = "[a-zA-Z]+=([a-zA-Z0-9\\u4E00-\\u9FA5'\\- ]+),?";
                    Pattern pattern = Pattern.compile(regular);
                    Matcher matcher = pattern.matcher(s);
                    int k = 0;
                    while (matcher.find()) {
                        // 处理数据
                        String str = matcher.group(1);
                        // 新建第n列
                        HSSFCell cell = row.createCell(k);
                        // 判断数据是否全数字
                        boolean temp = false;
                        for (int j = 0; j < str.length(); j++) {
                            if (Character.isDigit(str.charAt(j)) && str.indexOf('-') == -1) {
                                temp = true;
                            }
                        }
                        // 根据类型写入excel文档
                        if (temp) {
                            cell.setCellValue(Integer.parseInt(str));
                        } else {
                            // 数据处理
                            if (str.contains("'")) {
                                cell.setCellValue(str.replaceAll("'", ""));
                            } else {
                                cell.setCellValue(str);
                            }
                        }
                        k++;
                    }
                }
                try {
                    // 工作簿写出到该输出流
                    book.write(fos);
                    if (fos != null) {
                        // 关闭流
                        fos.close();
                    }
                    // 刷新流
                    fos.flush();
                    flag = true;
                } catch (IOException e) {
                    // TODO Auto-generated catch block
                    e.printStackTrace();
                }
            } catch (FileNotFoundException e1) {
                // TODO Auto-generated catch block
                e1.printStackTrace();
            }
            return flag;
        }
    }
    ```
