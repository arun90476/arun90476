    DateTimeFormatter formatter = DateTimeFormatter.ofPattern("EEEE, dd MMMM yyyy");
        LocalDate today = LocalDate.now();
        String formattedDate = today.format(formatter);
        System.out.println(formattedDate);
