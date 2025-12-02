 byte[] output = content.toString().getBytes("UTF-8");

        // Force download
        resp.setContentType("application/octet-stream");
        resp.setHeader("Content-Disposition", "attachment; filename=ModifiedFile.txt");
        resp.setContentLength(output.length);

        resp.getOutputStream().write(output);
