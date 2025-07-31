import 'package:flutter/material.dart';
import 'package:flutter_svg/flutter_svg.dart';
import 'package:hdfc_flutter_widgets/event_card/common/smart_pay_status.dart'; // Import the flutter_svg package

class PrimaryDetail extends StatelessWidget {
  /// Path to the SVG asset (e.g., "assets/icons/phone_bill.svg")
  final String prefixIconPath;

  /// Background color for the icon's circular container
  final Color prefixIconBackgroundColor;

  /// Main event name/title (e.g., "Mom's Phone Bill")
  final String title;

  final String subtitle;

  final String descriptionText;
  final String descriptionIconPath;

  const PrimaryDetail({
    super.key,
    required this.title,
    required this.prefixIconPath,
    required this.prefixIconBackgroundColor,
    required this.descriptionIconPath,
    required this.descriptionText,
    required this.subtitle,
  });
  @override
  Widget build(BuildContext context) {
    return Row(
      crossAxisAlignment: CrossAxisAlignment.start,
      children: [
        // Icon with circular background
        Container(
          padding: const EdgeInsets.all(8),
          decoration: BoxDecoration(shape: BoxShape.circle, color: prefixIconBackgroundColor),
          alignment: Alignment.center,
          child: SizedBox(
            width: 24,
            height: 24,
            child: SvgPicture.asset(
              prefixIconPath,
              // Add placeholderBuilder for error handling
              placeholderBuilder: (BuildContext context) =>
                  const Icon(Icons.error_outline, color: Colors.red),
            ),
          ),
        ),
        const SizedBox(width: 12),
        Expanded(
          child: Column(
            crossAxisAlignment: CrossAxisAlignment.start,
            children: [
              // Title text
              Text(
                title,
                style: const TextStyle(fontWeight: FontWeight.w600, color: Colors.black87),
                overflow: TextOverflow.ellipsis,
                maxLines: 2,
              ),
              const SizedBox(height: 4),
              // Description
              Text(
                descriptionText,
                style: TextStyle(color: Colors.grey.shade800),
                overflow: TextOverflow.ellipsis,
                maxLines: 2,
              ),
              const SizedBox(height: 20),
              SmartPayStatus(svgPath: descriptionIconPath, text: descriptionText),
            ],
          ),
        ),
      ],
    );
  }
}
